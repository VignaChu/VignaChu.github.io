---
title: DOM中的document对象
cover: ../../cover/little_don_cute.jpg

date: 2025-09-17T21:20:52+08:00
lastmod: 2025-09-16T20:12:50+08:00

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

document是JavaScript中最重要的对象之一，它代表了当前页面的根元素，可以用来获取页面的元素、属性、样式、事件等。

document对象是window对象的属性，因此可以直接通过window.document来访问。

# 常用方法

## 获取元素对象

1. `getElementById(id)`：通过元素的id属性获取元素对象。
2. `getElementsByName(name)`：通过元素的name属性获取元素对象。
   
    *注：name属性常用于表单元素的命名，仅对a, form, iframe, img, map, input, select, textarea等标签元素有效。不具有唯一性，不能用于css样式表中，但可以用于JavaScript。*

3. `getElementsByTagName(tagName)`：通过元素标签名获取元素对象。
4. `getElementsByClassName(className)`：通过元素的class属性获取元素对象。
5. `querySelector(selector)`：通过CSS选择器语法获取满足的第一个元素对象(不支持伪元素和部分伪类)
6. `querySelectorAll(selector)`：通过CSS选择器语法获取所有满足的元素对象(不支持伪元素和部分伪类)
   
## 创造新节点

1. `createElement(tagName)`：创建指定标签名的元素对象。
   
   `const li = document.createElement('li'); `
2. `createTextNode(text)`：创建文本节点。(纯文本，需要添加到元素中)
   ```javascript
   function addTextNode(text) {
        const newtext = document.createTextNode(text);
        const p1 = document.getElementById("p1");

        p1.appendChild(newtext); // 这个方法会在Element对象中讲到
      }
    ```
3. `createDocumentFragment()`：创建一个文档碎片对象，可以用来批量创建元素。
   
   其中文档碎片对象不属于文档树,插入文档树的时候会连带着将所有的子节点一起插入.可以先创建一堆节点,在将这些节点作为文档碎片的子节点一起插入文档树,能够提高性能。
   
    ```javascript
    var ul = document.getElementById("ul");
    var fragment = document.createDocumentFragment();
    for (var i = 0; i < 20; i++) {
      var li = document.createElement("li");
      li.innerHTML = "index: " + i;
      fragment.appendChild(li);
    }
    ul.appendChild(fragment);
    ```

## 获取

1. `document.documentElement`：返回当前文档的根元素。
2. `document.head`：返回当前文档的head元素。
3. `document.body`：返回当前文档的body元素。
4. `document.title`：返回当前文档的标题。
5. `document.URL`：返回当前文档的URL。
   
## 写入
1. `document.open();`：打开文档进行写入。
2. `document.write()`：向文档写入内容,如果文档没打开会自动调用，在打开后的文档使用会清空原有内容。
3. `document.writeln()`：向文档写入内容并换行。
4. `document.close()`：关闭文档。
```javascript
document.write("Hello, world!");
```


# 参考资料
- [封面图来源](https://safebooru.org/index.php?page=post&s=view&id=6030383)
- [HTML DOM Document querySelector()](https://www.w3schools.com/jsref/met_document_queryselector.asp)
- [HTML DOM Document 对象](https://www.runoob.com/jsref/dom-obj-document.html)
- [Document](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)
- [createDocumentFragment()用法总结](https://www.cnblogs.com/7qin/p/10639218.html)


