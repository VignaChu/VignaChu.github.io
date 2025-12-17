---
title: MIDI文件格式


date: 2025-11-22T09:16:52+08:00
lastmod: 2025-11-22T09:16:52+08:00
tags:
  - DALIY MUSIC
  - MIDI
  - Study
categories:
  - Study

math: true
mermaid: true

---


## MIDI文件格式

### 基本介绍

与常规的mp3/wav等音频文件不同，MIDI文件是一种基于时间的音频指令集合。它是一种标准格式，由一系列的**事件**（事件可以是音符、控制信息、轨道信息等）组成，这些事件按照一定时间顺序排列，可以用来**控制音乐播放器或硬件**播放音乐。本质上是一种**乐谱文件**而不是常规的波形文件。

MIDI文件中以**大端序**(big-endian)存储，即高位字节在前，需要从后向前读取。如果使用C++,C#等语言原生语法，由于默认是小端序(即从前往后读)，则需要手动转换。某些语言可能内置了支持读取大端序(如JAVA中的`DataInputStream`)的方法。

### 文件结构

MIDI文件以**块**(Chunk)为基本单位，如以下所示：
```
[4B ASCII 标识] + [4B 数据长度(N)] + [NB 数据内容]
```
最主要的块有:
- **文件头(MThd)**：在文件开始，全局只有一个，前14B是固定的
  - [0,4):固定为`4D 54 68 64`(即MThd)，标识这个是MIDI文件头
  - [4,8):头部数据的长度，固定为6
  - [8,10):格式类型(Format)，0表示单轨(所有数据挤在一起)，1表示多轨(并行播放)，此外还有罕见的2(多轨独立播放)
  - [10,12):轨道(Tracks)数量，表示后有多少MTrk块
  - [12,14):**时间基准(PPQ)**，最高位为0，后表示每个四分音符(一拍)存储多少tick，表示一拍被分成了几份，现代标准通常为960。PPQ决定了MIDI记录时间的精度，越高则能记录的细节越多。
- **轨道块(MTrk)**：存放音符数据
  - 格式：
    ```
    标识符: "MTrk" (0x4D 54 72 6B)
    长度:   4字节 (告诉你要往后读多少字节是属于这个轨道的)
    数据:   <Delta Time> <Event> <Delta Time>   <Event> ...
    ```
  -  循环构成“轨道块数据是由Delta Time和Event组成的无限循环，知道遇到结束事件：
     -  MIDI中的Delta TIME(即距离上事件过去时间)以变长存储，每个字节低7位存储数据，最高位作为标志位
        -  1：后面还有字节
        -  0：最后一个字节
     -  Event：事件，可以是音符、控制信息、轨道信息等。每个事件都有自己的格式，长度也不同。世间的第一个字节用于标识事件类型，后面跟着参数。
        - MIDI事件：(状态字节范围0x80~0xEF)status data1 data2(有些只有data1)
          - *注：下面n表示0~F，标记通道号，绑定不同的乐器*
          - 0x8n：Note Off，表示音符结束 
            - data1：音高(0~127),
            - data2：力度(0~127)
          - 0x9n：Note On，表示音符开始
            - data1：音高(0~127),
            - data2：力度(0~127)(*注：力度为零等效于Note Off*)
          - 0xAn：Polyphonic Key Pressure，表示多音符，可以为每个按键独立发送压力信息，以不同的粒度按下不同的键
            - data1：键号(0~127),
            - data2：力度(0~127)
          - 0xBn：Control Change，控制变化，用于动态调节乐器的各种参数
            - data1：控制器编号(0~127),（每个数字代表一个功能，但功能种类太多不予展示）
            - data2：控制器值(0~127)
          - 0xCn：Program Change，改变乐器
            - data1：乐器编号(0~127)
          - 0xDn：Channel Pressure，通道压力，用于控制通道的音量
            - data1：压力
          - 0xEn：弯音轮，用于模拟乐器的滑音
            - data1：低音节
            - data2：高音节
        - Meta事件`0xFF + [Type] + [Length (VLQ)] + [Data]`
          - 0x51：表示每拍微秒数(Tempo)，3B
          - 0x58：拍号
          - 0x03：显示轨道名字
          - 0x2F：结束事件
        - Sysex事件，这里不再介绍 
- **运行状态**
  -  MIDI文件可以保存当前的播放状态，包括当前的轨道、位置、音量、控制器等。
  -  规则：如果当前事件的 Status Byte 与上一个 MIDI 事件相同，可以省略 Status Byte
  
### 读取逻辑：
可以利用以下的逻辑进行读取：
1. 读取文件头
   - 验证 MThd。
   - 读取 Division (PPQ)。
   - 读取 TrackCount。

2. 读取每个轨道块(i from 0 to TrackCount)
- 验证 MTrk。
- 读取当前轨道数据长度。
- Current_Abs_Time = 0 (当前轨道的绝对时间 Ticks)。
- While (未读完轨道数据):
  - delta = read_vlq()
  - Current_Abs_Time += delta
  - status_byte = read_byte()
  - Check Running Status:
    - 如果 status_byte < 0x80:
      - 回退一个字节 (或者把这个字节当做 Data1)。
      - Status = Last_Status。
    - 否则: Last_Status = status_byte。
  - Switch (Status):
    - 0xFF (Meta): 读 Type -> 读 Length -> 读数据。如果是 Tempo，记录 (AbsTime, NewTempo)。
    - 0x80-0xEF (MIDI): 读 Data1 -> (根据Status类型决定是否读Data2)。如果是 NoteOn/Off，生成音符对象 (AbsTime, Pitch, Velocity, Channel)。
    - 0xF0/F7: 跳过。
- 时间转换 (Post-Processing):
  - 现在你有一堆 Ticks 为单位的事件。
  - 遍历 Tempo Map（速度变化表），结合 PPQ，将所有事件的 Ticks 转换为 Seconds 或 Milliseconds。
  - 公式：Time(ms) = (Ticks * MicrosecondsPerBeat) / (PPQ * 1000)。


### 存储方案

如果需要实现读取MIDI文件实现可视化音符流，可以参考以下格式存储：
```JSON
{
  "duration": 180.5, // 总秒数
  "tracks": [
    {
      "name": "Piano Right",
      "notes": [
        { "start": 1.2, "end": 1.8, "pitch": 60, "vel": 90 },
        { "start": 2.0, "end": 2.1, "pitch": 62, "vel": 85 }
      ]
    },
    {
      "name": "Drums",
      "notes": [...]
    }
  ]
}
```




