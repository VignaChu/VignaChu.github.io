---
title: WebAPI中的element对象
cover: ../../cover/蛮与伞.png
description: 介绍WebAPI中的Element对象。

date: 2025-09-19T16:32:52+08:00
lastmod: 2025-09-17T20:12:50+08:00

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

 element对象对应网页的HTML元素。每一个HTML元素，在DOM树上都会转化成一个element节点对象，因此通过document获取的元素对象本质上都是element对象，可以直接调用element对象的方法和属性。

# 属性

1. id:返回元素的id,可读写;
2. children:返回元素的子元素集合,只读;
3. className:返回元素的class属性值,可读写，返回一个字符串，每个类之间用空格分开;
4. classList:返回元素的classList对象，可读写，classList对象是一个类列表，可以对元素的类进行增(`add()`)删(`remove()`)改(`toggle()`*注:本方法用于翻转状态，即有则删除、无则添加*)查(`contains()`);
5. **innerHTML**:返回元素的innerHTML内容,可读写, 会将其中的HTML代码渲染;
6. innerText:返回元素的innerText内容,可读写, 会将其中的HTML代码渲染为纯文本;
7. style.属性:返回元素的style,可读写, 可以设置元素的CSS样式;

# 方法
1. focus():使元素获得焦点，即被点击的样子;
2. blur():使元素失去焦点;
3. remove():从DOM中移除元素;
4. append():插入多个节点，字符串等(用逗号分隔开)
5. appendChild():向元素内部添加一个子元素;
6. after():在元素父后面插入一个元素(即父节点上加一个在本节点后的节点);
7. children():返回元素的子元素只读集合;
8. **addEventListener()**:添加事件监听器;
9. **click()**:触发点击操作;
10. **getAttribute("属性名")**:获取元素的某属性值，此外还有set,remove,create,has等方法。



# 参考资料
- [封面图来源](https://safebooru.org/index.php?page=post&s=view&id=6059577)
- [DOM中Element对象常用属性与方法大全](https://blog.csdn.net/weixin_44992737/article/details/125296017)
- [HTML DOM Element 对象](https://www.w3school.com.cn/jsref/dom_obj_all.asp)
- [Element](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)

