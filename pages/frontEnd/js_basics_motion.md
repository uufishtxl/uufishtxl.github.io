---
title: JS基础入门之运动
catalog: true
tags: 
  - javascript
permalink: js_basics_motion_part1.html
folder: frontEnd
summary: JavaScript Basics
---

## offset 属性 | offset dimension

![offset dimension](img/javascript/js_animation_offset_dimension.png)



## 客户区大小 client dimension

是指元素内容及其内边距所占据的空间的大小。

![client dimension](img/javascript/js_animation_client_dimension.png)

比如说，如果要了解`body`元素的客户区大小，可以这么做：`document.documentElement.clientHeight`，`document.documentElement.clientWidth`。


## 滚动大小 scroll dimension

-   `scrollHeight`: 没有滚动条的情况下（就是假设有内容所在的空间足够大，大到不用滚动条就能全部显示内容），元素内容的总高度
-   `scrollWidth`: 没有滚动条的情况下，元素内容的总宽度
-   `scrollLeft`: 被隐藏的内容区域左侧的像素数
-   `scrollTop`: 被隐藏的内容区域上方的像素数

![client dimension](img/javascript/js_animation_scroll_dimension.png)

带有垂直滚动条的页面的总高度就是：`document.documentElement.scrollHeight`。

对于不包含滚动条的页面而言，scrollWidth 和 scrollHeight 与clientWidth、clientHeight之间的关系并不明确。

- Firefox: 两组属性相等，但是大小代表文档内容区域的实际尺寸，而非视口的尺寸。

- Opera, Safari 3.1 or above, Chrome: scrollWidth和scrollHeight等于视口大小，而clientWidth和clientHeight等于文档内容区域的大小。

- IE（在标准模式）：不相等。scrollWidth 和 scrollHeight等于文档内容区域的大小，而clientWidth 和 clientHeight 等于视口大小。

## 视口大小

IE8以上的方法：

`window.innerHeight` - 浏览器窗口内部高度 

`window.innerWidth` - 浏览器窗口内部宽度

标准模式下（CSS1Compat），inner可以视为包含滚动条的尺寸的视口。

而documentElement.client可以视为不包含滚动条尺寸的视口，两者在滚动条方向上相差17px;

混杂模式下（BackCompat）：ie10+的浏览器，三者的值是相同的。

### 关于混杂模式和标准模式

来源：https://www.cnblogs.com/qianlegeqian/p/4067635.html

检查方法：`document.compatMode`，可能得到两种值：

-   CSS1Compat: 标准模式
-   BackCompat: 混杂模式

`DOCTYPE`的一个重要作用，就是告诉浏览器，它该以何种<mark>模式</mark>呈现。出现混杂模式的原因：

-   不写`<!DOCTYPE html>`
-   <!DOCTYPE html>前面加上xml声明 <?xml version="1.0" encoding="utf-8"?> (IE6)
-   <!DOCTYPE html>和<?xml version="1.0" encoding="utf-8"?>之间加了（标签、文本、注释）(ie8以下都有，ie9以上未测)
-   <!DOCTYPE html>前面有（标签、文本、注释）(ie8以下都有，ie9以上未测)

之所以要区分混杂模式与严格模式，是因为w3c标准和IE传统标准对于盒模型的解析不一样等等。



