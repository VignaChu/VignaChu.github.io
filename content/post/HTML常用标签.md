---
title: HTML常用标签

cover: ../../cover/HTML1.jpg
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
## HTML头部定义
html的头部常以这种方式定义，一般编译器都会自动补全，需要的时候复制过来就行
```html
<!DOCTYPE html>
<html>
<head>
  <title>标题</title>
	<meta charset="UTF-8">
	<meta name="description" content="网站描述">
  <meta name="keywords" content="关键字">
  <meta name="author" content="作者">
  <link rel="icon" href="favicon.ico" />
  <link rel="stylesheet" href="style.css">
  <script src="script.js"></script>
</head>
```
## 常用标签概览

1. 标题标签 `<h1>~<h6>`
2. 段落标签 `<p>`
3. 换行标签 `<br>`: 用于在一行中插入换行符，不影响段落格式
4. 分割线`<hr>`: 用于分割内容，可以设置高度、颜色、宽度等属性
5. 链接标签 `<a>`: 用于创建超链接，可以设置链接地址、链接文本、链接目标窗口等属性
6. 图片标签 `<img>`: 用于插入图片，可以设置图片地址、宽度、高度、边框等属性
7. 列表标签 `<ul>`、`<ol>`、`<li>`: 用于创建无序列表、有序列表、列表项，可以设置列表项符号、缩进等属性
8. 表格标签 `<table>`、`<tr>`、`<td>`: 用于创建表格，可以设置表格宽度、高度、边框、背景色等属性
9. 表单标签 `<form>`、`<input>`、`<select>`、`<textarea>`: 用于创建表单，可以设置表单类型、名称、值、提示信息、是否必填等属性
10. 文字格式标签 `<b>`、`<i>`、`<u>`、`<strike>`、`<sup>`、`<sub>`: 用于设置文字的加粗、斜体、下划线、删除线、上标、下标样式
11. 块级元素标签 `<div>`、`<span>`: 用于创建块级元素和内联元素，可以设置元素宽度、高度、背景色、内边距、外边距等属性
12. 语义化标签 `<header>`、`<nav>`、`<main>`、`<section>`、`<article>`、`<aside>`、`<footer>`: 用于创建语义化标签，可以提高页面结构化、可读性、搜索引擎优化等效果
13. 其他标签 `<meta>`、`<link>`、`<script>`: 用于设置网页元数据、链接外部资源、嵌入脚本等

## 文字格式

html中插入文字格式标签可以设置文字的加粗、斜体、下划线、删除线、上标、下标样式。
1. `<b>`: 加粗
```html
<p>举例：<b>加粗文字</b></p>
```
2. `<i>`: 斜体
```html
<p>举例：<i>斜体文字</i></p>
```
3. `<u>`: 下划线
```html
<p>举例：<u>下划线文字</u></p>
```
4. `<sup>`: 上标
```html
<p>举例：<sup>上标文字</sup></p>
```
5. `<sub>`: 下标
```html
<p>举例：<sub>下标文字</sub></p>
```
6. `<ins>`: 下划线
7. `<del>`: 删除线
8. `<code>`: 代码
```html
<p>My favorite color is <del>blue</del> <ins>red</ins>!</p>
```

以上的文本样式标签均为行内样式。
## 创建连接

### 指定链接地址
html中创建连接主要使用`<a>`元素,**通过`href`标签指定链接地址**，可以有以下这几种类型：
1. 跳转到指定网页:
```html
<a href="https://www.baidu.com">百度</a>
```
1. 跳转到相对页面
```html
<a href="//example.com">相对于协议的 URL</a>
<a href="/zh-CN/docs/Web/HTML">相对于源的 URL</a>
<a href="./p">相对于路径的 URL</a>
```
3. 跳转到相同页面不同元素
```html
<!-- <a> 元素链接到下面部分 -->
<p><a href="#Section_further_down"> 跳转到下方标题 </a></p>

<!-- 要链接到的标题 -->
<h2 id="Section_further_down">更下面的部分</h2>

```
- 总结：
  - **普通的链接**：<a href="http://www.example.com/">链接文本</a>
  - **图像链接**： <a href="http://www.example.com/"><img src="URL" alt="替换文本"></a>
  - **邮件链接**： <a href="mailto:webmaster@example.com">发送e-mail</a>

### 指定打开方式

此外还可以通过`target`标签标记打开链接的位置，具体如下：

- _blank: 在新窗口或新标签页中打开链接。
- _self: 在当前窗口或标签页中打开链接（默认）。
- _parent: 在父框架中打开链接。
- _top: 在整个窗口中打开链接，取消任何框架。

### 下载对应文件

如果存在`download`标签，则变为下载对应文件而不是转到对应地址
```html
<p>
  <a href="#test" download="my.png">下载</a>
</p>

<img src="mine.png" alt="my image">
```

### 特殊的空连接
- `href="#"`:回到页面顶部
- `href="javascript:void(0)"`: 空连接，一般用于防止链接跳转
- `href=""`: 刷新当前页面
- `href="about:blank"`:打开空白页面

## 插入图片

定义图片的语法为:`<img src="url" alt="some_text" width="304" height="228">`，其中src属性用于指定图片的路径，alt属性用于指定图片无法显示时的替代文本。

可以直接在后面跟图片尺寸不用非得放到style里。
## 定义列表

### 无序列表

无序列表的语法为:`<ul> <li>item1</li> <li>item2</li> </ul>`，其中ul表示无序列表，li表示列表项。

```html
<ul>  
  <li>Coffee</li>  
  <li>Tea</li>  
  <li>Milk</li>  
</ul>
```

### 有序列表

有序列表的语法为:`<ol> <li>item1</li> <li>item2</li> </ol>`，其中ol表示有序列表，li表示列表项。

```html
<ol>  
  <li>Coffee</li>  
  <li>Tea</li>  
  <li>Milk</li>  
</ol>
```

### 自定义列表

自定义列表的语法为:`<dl> <dt>term1</dt> <dd>definition1</dd> <dt>term2</dt> <dd>definition2</dd> </dl>`，其中dl表示自定义列表，dt表示术语，dd表示定义(即对术语的后加解释)。

```html
<dl>  
  <dt>Coffee</dt>  
  <dd>A hot drink made from the roasted and ground seeds of a single coffee bean.</dd>  
  <dt>Tea</dt>  
  <dd>A hot drink made from the leaves of a tea plant.</dd>  
  <dt>Milk</dt>  
  <dd>A fluid obtained from the cow's milk.</dd>  
</dl>
```

## 定义表格

- 表格标签 `<table>`: 用于创建表格
- 表头标签 `<thead>`: 用于创建表头
- 表格行标签 `<tr>`: 用于创建表格行
- 表格标题标签 `<th>`: 用于创建表格标题
- 表格数据标签 `<td>`: 用于创建表格数据

```html
<table>
  <thead>
    <tr>
      <th>列标题1</th>
      <th>列标题2</th>
      <th>列标题3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>行1，列1</td>
      <td>行1，列2</td>
      <td>行1，列3</td>
    </tr>
    <tr>
      <td>行2，列1</td>
      <td>行2，列2</td>
      <td>行2，列3</td>
    </tr>
  </tbody>
</table>
```


## 定义表单

html中的表单主要用于获取用户输入的数据，相应的标签有 `<form>`、`<input>`、`<select>`、`<textarea>`。

- `<form>`: 用于创建表单,action决定数据提交的目标 URL，method决定提交方式，比如 GET 或 POST。
- `<label>`: 用于创建标签，可以为`<input>`、`<select>`、`<textarea>`等元素创建描述，也可使用for="id"与表单输入绑定。
- `<input>`: 用于创建输入框，可以设置类型、名称、值、提示信息、是否必填等属性，通过type属性可以设置输入框类型，通过name属性标记发送给后端
  - text: 单行文本输入框
  - password: 密码输入框
  - email: 邮箱输入框
  - radio: 单选按钮
  - checkbox: 复选框
  - submit: 提交按钮
- `<select>`: 用于创建下拉列表，可以设置名称、选项、默认选中项等属性
```html
<select name="cars">
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="mercedes">Mercedes</option>
  <option value="audi">Audi</option>
</select>
```
- `<button>`: 用于创建按钮，可以绑定点击事件，最好记得设置`type="button"`,否则会出问题
- `<textarea>`: 用于创建多行文本输入框，可以设置名称、值、提示信息、是否必填等属性

```html
<form>
  <label for="name">Name:</label> 
  <input type="text" id="name" name="name" required>
  <br>
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>
  <br>
  <label for="message">Message:</label>
  <textarea id="message" name="message" rows="4" cols="50" required></textarea>
  <br>
  <input type="submit" value="Submit">
</form>
```
## 块级元素和内联元素

1. `<div>`：用于定义块，通常用于批量管理块内的CSS格式，内部元素均为块级元素，每个元素占一行。
2. `<span>`：用于定义内联，通常用于对文本进行格式化，内部元素均为内联元素，多个元素可以并排显示。

```html
<div style="background-color: yellow;">
  <p>Hello World!</p>
  <span style="color: blue;">This is a block element.</span>
  <span style="color: red;">This is another block element.</span>
</div>

```
## 布局相关

传统的HTML语法中，常使用`<div>`、`<span>`、`<table>`等标签进行布局.

在页面中也可以通过`<iframe src="URL"></iframe>`插入新的页面。

## 字符实体


HTML中存在着一些预留字符，比如`<`、`>`、`&`等，这些字符在网页中有特殊的含义，如果直接在网页中使用这些字符，可能会导致网页显示异常。

为了解决这个问题，HTML引入了字符实体，字符实体是以“&”和“;”符号包围的特殊字符，它告诉浏览器以特殊方式显示这些字符。

常见的字符实体有：

- `&lt;`：小于号
- `&gt;`：大于号
- `&amp;`：与号
- `&quot;`：双引号
- `&apos;`：单引号
- `&nbsp`： 空格

```html
<p>This is a &lt;example&gt; of character entities.</p>
```

## 常用属性

- id：用于唯一标识一个元素，可用于JavaScript、CSS等。
- class：用于为元素指定多个类，可用于CSS样式表。
- style：用于为元素指定CSS样式。
- title：用于为元素添加提示信息,鼠标悬停时显示。
- href：用于指定超链接的链接地址(用于`<a>``<link>`标签)。
- src：用于指定外部资源的链接地址(用于`<img>`, `<script>`, `<iframe>`)
- alt：用于为图像提供替代文本，加载不出来的时候显示(用于`<img>`)
- type：用于指定`<input>`元素的类型(用于`<input>``<button>`)
- value：用于指定默认值(用于`<input>`,`<button>`,` <option>`)
- placeholder：用于指定默认值(用于`<input>`, `<textarea>`)

此外出于某种目的也可以自定义属性
- 格式：data-xxx-yyy：自定义属性，以data-开头，xxx为自定义名称，yyy为自定义值。
```HTML
<a data-link-type="game"
   data-game-id="1735700"
   href=""
   target="_blank">动物迷城</a>
```

## 参考资料
- [w3school](https://www.w3school.com.cn/)
- [菜鸟教程](https://www.runoob.com/)
- [MDN](https://developer.mozilla.org/zh-CN/)