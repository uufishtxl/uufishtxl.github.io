---
title: 基础知识：SVG / SYMBOL / USE
catalog: true
tags: 
  - vue
  - webpack
  - svg
permalink: vue_svg_symbol_use.html
folder: vue
summary: 了解什么是 SVG SYMBOL 和 SVG USE
---

### `svg symbols`

要利用`svg symbols`来建立图标体系，就需要了解其中的机制。

`<symbol>`其实是`<svg>`文档内的标签。一个`svg`文档可以包含多个`<symbol>`。利用`<symbol>`定义一组图形对象的模板，赋予它一个独一无二的`id`，对元素进行标识。这些图标对象会被深克隆到不可见的`DOM`中。

那么怎么去复制这些模板呢？这就要说到`<use>`了。

### `svg sprite`

包含多个`symbol`图像对象的`svg`就是一个`svg sprite`。

### `<svg>`的`viewBox`属性

`viewBox`定义了图标的宽高比。包含了四个值，前两位一般都是0，另外两个是`svg`图像的宽高比。

### `title`标签

还可以给每个图标一个`title`标签，增加访问行。

### `<use>`

要引用`symbol`定义的图标对象，同样需要用到`<svg>`标签。`<svg>`标签会包含一组`<use>`标签，使用`xlink:href`属性来指向要引用的图像对象内容的`id`，从而对它进行复制和渲染。

### 主要步骤

所以，用阿里的图标库来举例，我们要利用`svg symbol`来建立一套图标体系就需要：

1.  直接引入 `iconfont`生成的`iconfont.js`中的`<svg>`文档。

    ```html
    <svg style="display: none;">  <!--> 加上这个样式，是为了避免渲染 symbols <-->
      <symbol viewBox="0 0 24 24" id="heart"> <!--> 使用唯一id来对这个symbol进行标示<-->
        <path fill="#E86C60" d="M17,0c-1.9,0-3.7,0.8-5,2.1C10.7,0.8,8.9,0,7,0C3.1,0,0,3.1,0,7c0,6.4,10.9,15.4,11.4,15.8 c0.2,0.2,0.4,0.2,0.6,0.2s0.4-0.1,0.6-0.2C13.1,22.4,24,13.4,24,7C24,3.1,20.9,0,17,0z"> <!--> path才是图标本身的内容 <-->
        </path>
      </symbol>
    </svg>
    ```

2.  引用 `symbol id`，复制图标。可以利用`<use>`，进行无限次实例化展示。

    ```html
    <svg class="icon-class">
      <use xlink:href="#heart"></use>
    </svg>
    ```

#### 定义样式

在`<symbol>`中，我们可以看到`<path>`标签有一个`fill`属性，它定义了`svg`的填充颜色。如果要改变颜色，下面的定义方式是无效的，这是因为`svg`文档使用的是独立的 `DOM` 结构，`css`选择器无法获取它。

```css
.icon path {
  ...
}
```

要改变图标的填充颜色，首先需要确保`fill`属性不是**内联定义**的，如果有，就需要从模板中删除。

然后利用 `css` 继承的特点，通过定义`<svg>`标签的样式，来改变图标的样式。上面的例子中，就可以看到`<use>`标签中有定义`class`属性。

```css
.icon {
  fill: currentColor; /*currentColor表示将文本的颜色传递给 svg 图形，不需要担心会影响到其它元素，因为 fill 属性仅对 svg 有效果*/
}
```

### 限制

与浏览器的兼容性不佳，支持`IE 9.0+`，现代浏览器。