---
title: 使用JavaScript监听事件
cover: ../../cover/yukikaze.jpg
description: 介绍WebAPI中的事件监听。

date: 2025-09-20T20:43:15+08:00
lastmod: 2025-09-19T20:12:50+08:00

tags:
  - JavaScript
  - 前端学习
  - Study
categories:
  - Study

math: true
mermaid: true

---

# 引言

事件监听是一个必须掌握的知识点，可以实现复杂的脚本执行。

# 创建监听器

首先需要在一个element对象上绑定监听器:
```JavaScript
element.addEventListener(event, function, useCapture);
//可以通过getElementById()等方法获取element对象
```

第三个参数规定事件传播的方法是冒泡(false:先处理最内层元素的事件再处理外层的)还是捕获(true:相反)，默认为冒泡

此外还可以通过`removeEventListener()`移除监听器
# 常见的监听事件
## 鼠标事件:
## 键盘事件:
## 表单事件:
## 页面事件:
## 其他事件:

# event对象

## 常用event对象属性

event对象包含了与事件相关的各种信息，包括事件类型、事件源、鼠标位置、键盘按键、表单元素值等。
这些属性可以再事件监听器中的函数中使用。

1. event.target: 返回触发事件的元素;
2. event.currentTarget: 返回正在处理的元素;
3. event.type: 返回事件类型;
4. event.bubbles: 返回事件是否冒泡;
5. event.timeStamp: 返回从文档加载完成到事件触发的毫秒数;
6. event.isTrusted: 表示该事件是由用户触发还是JS脚本触发;
  
*以下的用于表单输入*
7. target.value:获取表单输入的值；

## 常用event对象方法
1. preventDefault():阻止默认行为;
2. stopPropagation():停止事件冒泡;
3. stopImmediatePropagation():阻止冒泡且阻止改元素其他的事件进行;
4. composedPath():返回事件的传播路径;
  



# 事件监听器优化策略：




# 参考资料
- [封面图来源](https://safebooru.org/index.php?page=post&s=view&id=2854457)
- [JavaScript之常用事件类型（全](https://blog.csdn.net/wangfei0225_/article/details/112984491)
- [JavaScript事件总结（最详细！）：事件监听器、event事件对象、事件分类、事件默认行为](https://www.cnblogs.com/qianduanLamp/p/16552978.html)
- [理解 JavaScript 事件监听的各种类型、使用方法与优化策略](https://juejin.cn/post/7435701496547049513)

