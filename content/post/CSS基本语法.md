---
title: CSS基本语法

cover: ../../cover/dragon_bubble1.jpg
date: 2025-09-13T21:56:52+08:00
lastmod: 2025-09-12T12:12:52+08:00
tags:
  - CSS
  - 前端学习
  - Study
categories:
  - Study

math: true
mermaid: true

---

# 杂谈 

之前学过一遍，但是忘了，今日来速通。

# 语法
```CSS
选择器{
    属性:值;
    ···
    /*注释*/
    属性:值;
}
```
# 选择器

- **标签选择器**：标签名称，如 `div` 。
- **类选择器**：.类名，如 `.class` 。
- **ID选择器**：#ID名，如 `#id` 。
- **通用选择器**：\* ，匹配所有元素。
- 分组选择器：多个选择器用逗号分隔，如 `h1, h2, h3` 。
- 属性选择器：选择器[属性]，如`*[title] `，`[attr="value"]`表示属性等于哪个值才选，与之类似还有`[attr~="value"]`(包含某个以空格分类的单词)、`[attr|="value"]`(属性值以某个值开头，后面可跟连字符)、 `[attr^="value"]`(属性值以某字符串开头)、`[attr$="value"]`(结尾)、`[attr*="value"]`(子串)。
- 后代选择器：选择器1 选择器2(选择器1内部元素或内部元素的内部元素)，如 `div p{background-color:blue}` 。
- 子元素选择器：选择器1 > 选择器2(选择器1的直接子元素)，如 `div > p{background-color:blue}` 。
- 相邻兄弟选择器：选择器1 + 选择器2(选择器1的下一个兄弟元素)，如 `h1 + h2{color:red}` 。
- 兄弟选择器：选择器1 ~ 选择器2(选择器1后面的所有兄弟元素)，如 `h1 ~ h2{color:red}` 。

# 添加

我喜欢直接外部css`<link rel="stylesheet" type="text/css" href="mystyle.css">`，这样比较清晰，其他不在这里讲。

# 属性

## 颜色

- `color`：设置文本颜色。
- `background-color`：设置背景颜色。
- `border-color`：设置边框颜色。

## 字体

- `font-family`：设置字体。
- `font-size`：设置字体大小。
- `font-weight`：设置字体粗细。
- `font-style`：设置字体风格。
- `text-decoration`：设置文本装饰。
- `text-align`：设置文本对齐方式。(center; left; right; justify;)
- `direction`:设置文本方向。(ltr; rtl;)
- `unicode-bidi`:设置文本方向。(normal; embed; bidi-override;)
- `text-decoration`:设置文本装饰。(none; underline; overline; line-through;)
- `line-height`：设置行高。
- `letter-spacing`：设置字符间距。
- `text-shadow`：设置文本阴影。（横 纵 (模糊) 颜色）

## 边框

- `border`：设置边框。
- `border-width`：设置边框宽度。
- `border-style`：设置边框样式，可以取以下值(dotted, dashed, solid, double, groove, ridge, inset, outset, none, hidden)，具体效果自己查。
- `border-radius`：设置边框圆角。
  
此外在边框后加修饰词可以指定哪条边框
```CSS
p {
  border-top-style: dotted;
  border-right-style: solid;
  border-bottom-style: dotted;
  border-left-style: solid;
}
```
- margin：设置外边距。
```CSS
p {
  margin-top: 100px;
  margin-bottom: 100px;
  margin-right: 150px;
  margin-left: 80px;
}
```

或简写(上右下左)：
```CSS
p {
  margin: 100px 150px 100px 80px;
}
```
- padding：设置内边距，语法与外边距一致。

## 背景

- `background-image`：设置背景图片。
- `blackground-color`：设置背景颜色。
- `background-repeat`：设置背景重复。(repeat-x; repeat-y; no-repeat;)
- `background-position : [水平][垂直]` 设置背景位置(只写一个第二个默认为center)。(left/top/center/right/bottom)
- `background-position : 水平% 垂直%`和容器的百分点对齐
- `background-position : 水平单位 垂直单位`位移多少，正向右下，负向左上。
- *三条background属性可以混写，也可简写(在此不介绍，个人觉得不直观)*
- `background-attachment`：设置背景是否随页面滚动而滚动。(scroll; fixed;)
- height、width：设置背景大小。
- max-width、max-height：设置背景最大大小。
- min-width、min-height：设置背景最小大小。

# 排版
- `display`：设置元素的显示方式。(block; inline; inline-block; none;)
- `visibility`：设置元素的可见性。(visible; hidden;)

display:none直接删除不占据空间
visibility:hiden占据空间，空出一块位置
可以通过按钮绑定脚本修改元素的style属性，实现显示隐藏。
- `z-index`：设置元素的堆叠顺序。（数值越大越靠前，可以为正为负）如果没定义这个属性默认最后定义的在上面
- `overflow`：设置元素溢出处理。(visible溢出到外面; hidden溢出的隐藏; scroll加滚动条; auto溢出才加滚动条;)后加-x或-y表示只在x或y轴溢出。
- `float`:元素在容器的哪里?（left; right; none;)
- `clear`：元素的两侧不允许其他元素。(left; right; both; none;)
# 参考资料
- [w3school](https://www.w3school.com.cn/)