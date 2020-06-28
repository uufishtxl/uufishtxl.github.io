---
title: 计算属性
catalog: true
tags: 
  - vue
permalink: vue_note_computed.html
folder: vue
summary: 梁灏 《Vue.js》 实战笔记
---

模板内的表达式常用语简单运算，逻辑较复杂时，常用更易于维护的计算属性来解决问题。

## 什么是计算属性

前面章节中有个例子：

```html
<div id="app">
  {% raw %}{{ text.split('.').reverse().join('') }}{% endraw %}
</div>
```

改写：

```html
<div id="app">
  {% raw %}{{ reversedText }}{% endraw %}
</div>
var app = new Vue({
	el: '#app',
  data: {
  	text: '123, 456'
  },
  computed: {
  	reversedText: function() {
    	return this.text.split(',').reverse().join(',');
    }
  }
})
```

## 计算属性的用法

### 依赖多个Vue实例中的数据重新执行计算属性

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/8L9x3jm5/1/)

### `getter` 和 `setter`

上面的例子都是用了计算属性的默认用法，也就是利用getter来读取。需要时，也可以提供一个setter函数，当手动修改计算属性的值就像修改一个普通数据那样时，就会触发setter函数，执行一些自定义操作。

[使用计算属性的setter函数](https://jsfiddle.net/edith_tang/ucsz3rne/15/)

{% include note.html content="实际应用中，很少会用到setter函数。这时候，就不需要分别声明`get`和`set`函数，可以直接使用默认的写法。" %}

### 应用场景

#### 文本插值

上述例子都将计算属性应用在文本插值。

#### `class`属性和内联样式 style

[链接：稍后补全](vue_note_computed.html)


### 小技巧

-   计算属性可以依赖其他计算属性

-   计算属性不仅可以依赖当前Vue实例的数据，还可以依赖其他实例的数据  
    [《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/9awdLbzj/4/)

## 计算属性缓存

计算属性所完成的最终效果，用`methods`也能实现，比如下面的例子。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/9awdLbzj/7/)

甚至用methods，还能传入参数，似乎更为灵活。那么两者有什么区别，为什么要用计算属性呢？

原因就是：***计算属性是基于它的依赖缓存的***（(>^ω^<) 喵喵喵？）

> 一个计算属性所依赖的数据发生变化时，它才会重新取值，所以 `text` 只要不发生变化，计算属性也就不更新。
> 
> 使用计算属性还是 methods 取决于你是否需要缓存，当遍历大数组和做大量计算时，应当使用计算属性，除非你不希望得到缓存。



