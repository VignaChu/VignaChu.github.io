---
title: HTML初学笔记

cover: ../../cover/HTML2.jpg
date: 2025-11-04T12:30:52+08:00
lastmod: 2025-11-04T12:30:50+08:00
tags:
  - HTML
  - 前端学习
  - Study
categories:
  - Study

math: true
mermaid: true

---
## 新增标签

### 布局相关
HTML5语法引入了一些新的标签来定义布局，这些标签可以帮助我们更好地控制页面的结构和样式。
1. `<header>`：用于定义页眉，通常包含网站的logo、导航、搜索框等。
2. `<nav>`：用于定义导航，通常包含网站的主要导航链接。
3. `<main>`：用于定义主要内容，通常包含页面的主要内容。
4. `<section>`：用于定义区域，通常包含页面的某个区域。
5. `<aside>`：用于定义侧边栏，通常包含页面的侧边栏内容。
6. `<footer>`：用于定义页脚，通常包含网站的相关信息。
```html
<header>
  <h1>My Website</h1>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
    </nav>
  <form>
    <input type="text" placeholder="Search...">
    <button type="submit">Go</button>
  </form>
</header>
```
### 绘图区域

#### <canvas>
HTML5添加了<canvas>来创建绘图区域，可以通过JS语法绘制内部形状,通过width/height属性设置大小：

```HTML
<canvas id="myCanvas"></canvas>
 
<script type="text/javascript">
var canvas=document.getElementById('myCanvas'); // 获取canvas元素
var ctx=canvas.getContext('2d'); // 申请2D上下文
ctx.fillStyle='#FF0000'; // 设置填充颜色
ctx.fillRect(0,0,80,100); // 绘制图像
</script>
```

常用2D绘制方法：

下面给出一张“**一张表扫完 Canvas2D 常用绘图接口**”的速查表，左侧是**任务/功能**，右侧是**最常用/相关联的 API**。  
只列“日常开发 90 % 会碰到的”，按字母序排，一眼定位。

| 任务 / 功能 | 关键调用（常用简写） |
|-------------|----------------------|
| 圆弧 | `arc(x, y, r, start, end)` / `arcTo(x1, y1, x2, y2, r)` |
| 贝塞尔曲线 | `quadraticCurveTo(cpX, cpY, x, y)` / `bezierCurveTo(cp1X, cp1Y, cp2X, cp2Y, x, y)` |
| 裁剪区域 | `clip()`（基于当前路径） |
| 清除矩形 | `clearRect(x, y, w, h)` |
| 虚线 | `setLineDash([5, 3])` / `lineDashOffset = 0` |
| 椭圆 | `ellipse(x, y, rx, ry, rot, start, end)` |
| 填充矩形 | `fillRect(x, y, w, h)` |
| 填充路径 | `fill()` / `fill(fillRule)` |
| 填充文字 | `fillText(text, x, y [, maxWidth])` |
| 渐变色 | `createLinearGradient` / `createRadialGradient` |
| 图片绘制 | `drawImage(img, dx, dy, dw, dh)` |
| 图片数据 | `getImageData` / `putImageData` / `createImageData` |
| 线帽/线Join | `lineCap = 'butt|round|square'` / `lineJoin = 'miter|round|bevel'` |
| 线段 | `moveTo(x, y)` + `lineTo(x, y)` + `stroke()` |
| 线宽 | `lineWidth = value` |
| 测量文字 | `measureText(text).width` |
| 全局透明度 | `globalAlpha = 0~1` |
| 合成模式 | `globalCompositeOperation = 'source-over'|'multiply'|'screen'|...` |
| 保存/还原 | `save()` / `restore()` |
| 阴影 | `shadowColor` / `shadowBlur` / `shadowOffsetX` / `shadowOffsetY` |
| stroke 矩形 | `strokeRect(x, y, w, h)` |
| stroke 路径 | `stroke()` |
| stroke 文字 | `strokeText(text, x, y [, maxWidth])` |
| 变换矩阵 | `translate(x, y)` / `rotate(angle)` / `scale(sx, sy)` / `setTransform(a,b,c,d,e,f)` |
| 图案填充 | `createPattern(img, 'repeat|repeat-x|repeat-y|no-repeat')` |
| 文字字体 | `font = '16px Arial'` / `textAlign = 'left|center|right'` / `textBaseline = 'top|middle|bottom'` |

把这张表贴在键盘旁，写 Canvas2D 基本不用再翻 MDN。

#### SVG
使用XML语言描绘矢量图，可以为元素加上JS事件处理器，但不能保存为图像，且性能消耗大。

1. **基本语法**
  
```xml
<svg width="200" height="200" viewBox="0 0 100 100"> 
  <circle cx="50" cy="50" r="40" fill="tomato" stroke="#000" stroke-width="3"/> 定义元素(可挂监听器)
</svg>
``` 
2. 常用元素

| 标签           | 作用      | 关键属性                                      |
| ------------ | ------- | ----------------------------------------- |
| `<rect>`     | 矩形      | `x y width height rx ry`                  |
| `<circle>`   | 圆       | `cx cy r`                                 |
| `<ellipse>`  | 椭圆      | `cx cy rx ry`                             |
| `<line>`     | 直线      | `x1 y1 x2 y2`                             |
| `<polyline>` | 折线      | `points="x0,y0 x1,y1 …"`                  |
| `<polygon>`  | 封闭多边形   | `points="…"` 自动闭合                         |
| `<path>`     | 万能路径    | `d="M moveto L lineto C curveto Z close"` |
| `<text>`     | 文字      | `x y dx dy rotate textLength`             |
| `<image>`    | 嵌入位图    | `href xlink:href x y width height`        |
| `<g>`        | 编组      | 可统一 transform / 样式                        |
| `<defs>`     | 定义复用资源  | 渐变、滤镜、图形模板                                |
| `<use>`      | 引用 defs | `href="#id" x y`                          |
| `<symbol>`   | 视图模板    | 与 `<use>` 搭配做 sprite                      |

同样也可以用CSS，JS修饰

- **渐变**
```xml
<defs>
  <linearGradient id="g" x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%" stop-color="#ff0"/>
    <stop offset="100%" stop-color="#f0f"/>
  </linearGradient>
</defs>
<rect width="100" height="50" fill="url(#g)"/>
```
- **滤镜**
```xml
<filter id="blur">
  <feGaussianBlur stdDeviation="3"/>
</filter>
<circle cx="50" cy="50" r="40" filter="url(#blur)"/>
```

### 其他标签

- `<mark>`:内联，高亮背景

## HTML5新特性

### 拖放

H5支持将一个元素拖到另外一个元素中，通过给元素加 draggable → 监听 drag 事件 → 在 drop 里拿数据

下面是一段示例代码：
```html
<div id="box" draggable="true">拽我</div> //定义dragable标签
<div id="bin">放这儿</div>

<script>
const box = document.getElementById('box');
const bin = document.getElementById('bin');

// 拖拽开始
box.addEventListener('dragstart', e => {  // 在可拖拽的元素添加dragstart监听器
  e.dataTransfer.setData('text/plain', e.target.id);   // 存数据
  e.dataTransfer.effectAllowed = 'move';               // 光标样式
});

// 经过放置区必须阻止默认行为，否则浏览器拒收
bin.addEventListener('dragover', e => e.preventDefault());

// 放下
bin.addEventListener('drop', e => { // 在目的地定义drop监听器
  e.preventDefault();
  const id = e.dataTransfer.getData('text/plain');     // 读数据
  const el = document.getElementById(id);
  el.parentNode.removeChild(el);                       // 举例：扔进垃圾桶
  bin.textContent = '已删除';
});
</script>
```

### 地理定位

H5可通过Geolocation API 来获取当前用户的位置，但需要用户同意才可以
```javascript
// 拿到页面里用于显示结果的元素（假设 <p id="demo"></p>）
var x = document.getElementById("demo");

/**
 * 入口函数：点击按钮时调用
 * 1. 判断浏览器是否支持地理定位
 * 2. 支持：申请获取当前位置
 * 3. 不支持：直接给出提示
 */
function getLocation() {
    if (navigator.geolocation) {
        /* 官方 API：getCurrentPosition(
               成功回调,
               失败回调（可选）,
               配置对象（可选）
           )
           下面只传了成功回调，最简单写法 */
        navigator.geolocation.getCurrentPosition(showPosition);
    } else {
        x.innerHTML = "该浏览器不支持获取地理位置。";
    }
}

/**
 * 成功获取位置后的回调函数
 * @param {Position} position  - 由浏览器传入的地理位置对象
 */
function showPosition(position) {
    /* position.coords 下存放所有坐标信息
       常用：latitude 纬度、longitude 经度
       其它：accuracy 精度（米）、altitude 海拔、speed 速度等 */
    x.innerHTML = "纬度: " + position.coords.latitude +
                  "<br>经度: " + position.coords.longitude;
}
``` 

### 新的多媒体元素

H5添加了一系列的多媒体标签：
1. `<video>`:播放视屏，提供了播放、暂停和音量控件等功能；
```HTML
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
您的浏览器不支持Video标签。
</video>
``` 
此外还可以利用JS控制视频：
```HTML
<div style="text-align:center"> 
  <button onclick="playPause()">播放/暂停</button> 
  <button onclick="makeBig()">放大</button>
  <button onclick="makeSmall()">缩小</button>
  <button onclick="makeNormal()">普通</button>
  <br> 
  <video id="video1" width="420">
    <source src="mov_bbb.mp4" type="video/mp4"> 
    // 播放能播放的，如果都可以则任选一个
    <source src="mov_bbb.ogg" type="video/ogg">
    您的浏览器不支持 HTML5 video 标签。
  </video>
</div> 

<script> 
var myVideo=document.getElementById("video1"); 

function playPause()
{ 
	if (myVideo.paused) 
	  myVideo.play(); 
	else 
	  myVideo.pause(); 
} 

	function makeBig()
{ 
	myVideo.width=560; 
} 

	function makeSmall()
{ 
	myVideo.width=320; 
} 

	function makeNormal()
{ 
	myVideo.width=420; 
} 
</script> 
```
2. `<audio>`：播放音频，提供了播放、暂停和音量控件等功能；
```HTML
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>
```
### 表单相关

#### 更多的表单输入 
h5添加了一系列新的表单输入:
- color：拾色器
- date：日历
- datetime：日期时间
- datetime-local：本地日期时间
- email：邮箱输入
- month：月份
- number：数字输入,通过以下修饰：
  disabled	规定输入字段是禁用的
  - max	规定允许的最大值
  - maxlength	规定输入字段的最大字符长度
  - min	规定允许的最小值
  - pattern	规定用于验证输入字段的模式
  - readonly	规定输入字段的值无法修改
  - required	规定输入字段的值是必需的
  - size	规定输入字段中的可见字符数
  - step	规定输入字段的合法数字间隔
  - value
- range：滑动条,使用以下属性修饰
  - max - 规定允许的最大值
  - min - 规定允许的最小值
  - step - 规定合法的数字间隔
  - value - 规定默认值
- search：搜索框
- tel：电话号码
- time：时间
- url：网址输入
- week：星期

### 限制表单输入
H5可以通过`<datalist>`元素限制表单输入
```HTML
<input list="browsers"> // 通过list属性关联datalist元素
 
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
```
### 计算输入的输出
H5通过`<output>`元素计算输入的输出
```HTML
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
<input type="range" id="a" value="50">100 +
<input type="number" id="b" value="50">=
<output name="x" for="a b"></output>
</form>
```
### 输出时提示

`<input>`的*placeholder*属性用于在获得焦点前显示文本
```HTML
<input type="text" placeholder="请输入内容">
```

*注：新增的关于存储相关的内容单独一篇文章讲*

## 参考资料
- [w3school](https://www.w3school.com.cn/)
- [菜鸟教程](https://www.runoob.com/)
- [MDN](https://developer.mozilla.org/zh-CN/)