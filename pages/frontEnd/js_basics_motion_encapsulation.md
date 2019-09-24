---
title: 透明度改变 / 多div框宽度伸缩
catalog: true
tags: 
  - javascript
  - animation
permalink: js_animation_encapsulation.html
folder: frontEnd
summary: 改变透明度 封装一个能够支持各种样式属性变化的函数
---

## 透明度的改变

透明度的改变和变速运动没有很大的区别。

但是，需要注意的是，`filter`属性只适合标准浏览器。为了兼容IE8及以下版本的服务器，需要使用`alpha`属性。

## 多div框宽度伸缩

需求：有多个div框，要求封装一个函数，当鼠标对这些div框做移入和移出操作时，将改变div框的宽度。

需要注意以下几点：

-   需要为每个div框设置独立的计时器。只要获取一个包含所有div框的数组，然后对它进行遍历，并未每个元素设置独立的计时器(array[i].timer)即可。

-   为遍历到的元素绑定计时器时，obj形参位置可以传入this，表示调用该函数的对象。

## offset dimension的副作用

`offsetWidth`是指内容宽度（`obj.style.width`）和左右边框的总和。那么，当速度很小（比如说-1）的时候，如果直接用`obj.style.width = offsetWidth + speed + 'px'`来改变宽度的话，虽然负数的速度是想要缩小宽度，但是计算下来实质上却是在增加宽度。所以这种情况下，`offsetWidth`明显不适用了。

## div框完成两个连续的操作

需求：鼠标移入时，增加边框宽度到100像素，完成后，伸长div框的高度到400像素。移出时，先缩小高度，然后缩小边框宽度。

0.   考虑到是两个连续的操作，所以要在封装的运动框架中传入一个回调函数，作为参数。

1.   获取起点/当前css的值。  
     {% include note.html content="需要根据css值是否为opacity，来调整css的值。如果是opacity，需要乘以100。" %}

2.   计算速度。

3.   要考虑到如果传入了回调函数，那么需要在结束计时器时（到达目标位置），调用回调函数。

4.   定义运动时，要考虑到如果是opacity属性，如何兼容不同的浏览器。 
     {% include note.html content="css属性是以引号形式传入的。所以显然，不能用dot notation来定义行间样式的属性了。所以要用`obj.style[attr]`的形式进行定义。" %}
     {% include note.html content="css用驼峰式。比如`border-width`，就要写成`borderWidth`" %}