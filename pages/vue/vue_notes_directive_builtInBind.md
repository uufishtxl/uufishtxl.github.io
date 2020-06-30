---
title: 内置指令
catalog: true
tags: 
  - vue
permalink: vue_note_directive_bind_builtin.html
folder: vue
summary: 梁灏 《Vue.js》 实战笔记
---

## 基本指令

### `v-cloak`

`v-cloak`不需要表达式，它会在Vue实例结束编译时从绑定的 HTML 元素上移除，经常和 CSS 的 `display: none;` 配合使用。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/fdyqa7xe/3/)

我的理解就是：*如果网速很慢，网页还没完全加载的时候，就会出现 {% raw %}{{message}}{% endraw %}的字样，直到 Vue 实例创建完成，编译后 DOM 才会被替换。所以可以用v-cloak来解决问题。但是因为加了v-cloak后，屏幕会有闪动，这时候就要配合CSS里指定 `[v-cloak] {display: none;}`来食用更佳。*

一般来说，`v-cloak`是一个解决初始化慢导致页面闪动的最佳实践，适用于简单的项目。当需要用到 webpack 或者 vue-router 时，项目 HTML 结构只有一个空的 `div` 元素，剩余的内容都会由路由去挂载不同的组件完成，所以不再需要 `v-cloak`。

### `v-once`

同样不需要表达式。作用是：定义它的元素或组件只渲染一次，包括元素或组件的所有子节点。首次渲染后，不再随数据的变化重新渲染，将被视为静态内容。

在业务中，很少会使用。

## 条件渲染指令

### `v-if`, `v-else-if`, `v-else`

根据表达式的值在 DOM 中渲染或销毁元素/组件。`v-else-if` 和 `v-else` 必须紧跟 `v-if`。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/2etoLmwd/4/)

如果一次判断多个元素，可以在 Vue.js 内置的 `<template>`元素上使用条件指令，最终渲染结果不会包含该元素。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/xfrzt03d/4/)

Vue 在渲染元素时，出于效率考虑，会尽可能复用已有的元素而非重新渲染，比如下面的实例：

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/1jzLh6ka/8/)

输入内容后点击切换内容，会发现虽然 DOM 变了，但是输入框中的内容并没有发生变化，而只是替换了 `placeholder`的内容。

如果你不希望这样做，可以使用 Vue.js 提供的 key 属性，它可以让你决定是否要复用元素，key的值是唯一的。

给两个`<input>`元素都增加 key 后，就不会复用了，切换类型时键入的内容也会被删除，不过`<label>`元素仍然是被复用的，因为没有添加 key 属性。

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/1jzLh6ka/11/)

### `v-show`

用法基本与`v-if`一致，但是是用来改变元素的 CSS 属性 display。当 `v-show` 表达式的值为 `false`时，元素会隐藏，查看 DOM 结构会看到元素上加载了内联样式 `display: none;`。

`v-show`不能在`<template>`上使用。


[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/y8mf5rwx/3/)


### `v-for`

#### 对数组进行遍历

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/pgajLxdu/7/)

1.  如何理解：books 是实例中的数据，book是数组中的元素的别名，循环出的每个<li>都可以访问对对应的当前数据 book
2.  也可依用book of books

##### 支持一个可选参数作为索引

`<li v-for="(book, index) in books">{{ index + 1 }} - {{ book.name }}</li>`

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/0ey5odbp/3/)

#### 在`<template>`上使用

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/0ey5odbp/17/)

#### 对 Object 数据属性的遍历


[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/xoayemfg/6/)

遍历对象时，有两个可选参数，分别是**键名**和**索引**。

**键名**就是 Object 数据中的 key 的名称。

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/xoayemfg/10/)

#### 迭代整数

[Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/pqmyh6j4/2/)

### 数组更新

Vue 的核心是数据与视图的双向绑定，当我们修改数组时，Vue 会检测到数据的变化，所以用 v-for 渲染的视图也会立即更新。Vue 包含了一组观察数组变异的方法，使用它们改变数组也会触发视图更新：

-   `push()`
-   `pop()`
-   `shift()`
-   `unshift()`
-   <b data-toggle="tooltip" data-original-title="{{site.data.vue_dict.ary_splice}}">`splice()`</b>
-   `sort()`
-   `reverse()`

用法应该和[这里](js_methods.html)类似。

[例子](https://jsfiddle.net/edith_tang/oezs6ygw/10/)示范了如何用`push()`来实现数组和视图的更新。

以上方法会改变被这些方法调用的原始数组，有些方法不会改变原数组，比如：

-   `filter()`
-   `concat()`
-   `slice()`

它们返回的是一个新数组，在使用这些非变异方法时，可以用新数组来替换原数组。

[例子](https://jsfiddle.net/edith_tang/0mrnq9h5/11/)示范了如何用`filter()`来产生一个新数组并且替换就数组，以更新视图。

同样，Vue不会重新渲染整个列表，而会最大化复用 DOM 元素。也就是说，替换中，含有相同元素的项不会被重新渲染，因此不用担心性能的问题。

但是，Vue 不能检测到下面两种数组的变更方法，更不用说触发视图更新了。

-   通过索引直接设置项，比如 `this.books[3] = {}`
-   修改数组长度，比如 `this.books.length = 5`

第一个问题的解决方法：

1.  [使用 Vue 内置的 set 方法](https://jsfiddle.net/edith_tang/0mrnq9h5/15/)。
    {% include note.html content="如果是webpack的方法，还有别的事情要处理。因为暂时没有学到webpack的相关知识，所以后面再补充，*P42*" %}

2.  用<b data-toggle="tooltip" data-original-title="{{site.data.vue_dict.ary_splice}}">`splice()`</b>，[查看实例](https://jsfiddle.net/edith_tang/mz9sydxu/6/)。  
    > `array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`

第二个问题也可以用`splice()`来解决。

### 过滤与排序

如果不想改变原数组，而是想要通过一个数组的副本来做过滤或排序的显示，可以使用计算属性来返回过滤或排序后的数组。

[例子](https://jsfiddle.net/edith_tang/s0wrbq8g/10/)

## 方法与事件

### 基本用法

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/ftycx0nb/11/)

书里解释了`@click="methodName"`是否需要加上`()`的问题，原文如下：

> 需要注意的是，`@click`调用的方法名后可以不跟括号。此时，如果该方法有参数，默认会将原生事件对象 event 传入，可以尝试修改为`@click="handleAdd"`，然后在 `handleAdd` 中打印出 `count` 参数看看。在大部分业务场景中，如果方法不需要传入参数，为了简便，可以不写 `()`。

这么理解更简单：*触发函数是否需要加上`()`，取决于定义函数是否带参数，而不取决于你传不传参数*。

下面这句话暂时无法理解：

> 这种在 HTML 元素上监听事件的设计看似将 DOM 与 JavaScript 紧耦合，违背分离的原理，实则刚好相反。因为通过 HTML 就可以知道调用的是哪个方法，将逻辑与 DOM 解耦，便于维护。最重要的是，当 ViewModel 销毁时，所有的事件处理器都会自动删除，无需自己清理。

#### `$event`：访问 DOM 原生事件

Vue 提供了一个特殊变量`$event`，用于访问原生 DOM 事件，例如下面的实例可以阻止链接打开：

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/xju9tqdk/4/)

#### 知识插播：紧耦合和解耦  \| Tight Coupling & Decoupling

> ***紧耦合 (tight coupling)***
>
>紧耦合就是模块或者系统之间关系太紧密，存在相互调用。紧耦合系统的缺点在于更新一个模块的结果导致其它模块的结果变化，难以重用特定的关联模块。
>
> ***解耦 (decoupling)***
>
> 耦合是指两个或两个以上的体系或两种运动形式间通过相互作用而彼此影响以至联合起来的现象。 解耦就是用数学方法将两种运动分离开来处理问题，常用解耦方法就是忽略或简化对所研究问题影响较小的一种运动，只分析主要的运动。

### 修饰符

前面阻止原生事件的功能，也可以通过修饰符实现。

要使用修饰符，需要在@绑定的事件后加小圆点`.`，再跟一个后缀。Vue 支持以下修饰符：

-   `.stop`：阻止事件冒泡 - `<a @click.stop="handle"></a>`
-   `.prevent`：阻止事件的默认行为 - `<a @click.prevent="handle"></a>`
-   `.capture`：添加事件侦听器时使用事件捕获模式 - `<div @click.capture="handle">...</div>`
-   `.self`：只当事件在该元素本身（而不是子元素）触发时触发回调 - `<div @click.self="handle">...</div>`
-   `.once`：只触发一次，组件同样适用 - `<div @click.once="handle">...</div>`

#### 按键修饰符

在表单元素上监听键盘事件时，还可以使用***按键修饰符***，比如：

`<input @keyup.13="submit">`

仅在`keyCode`是13时调用`vm.submit`。

#### 自定义按键

也可以自己配置具体按键：

`Vue.config.keyCode.f1 = 112;`

全局定义后，就可以使用`@kepup.f1`。

#### 快捷访问按键

Vue 还提供了一些快捷名称：

-   .enter
-   .tab
-   .delete (捕获*删除*和*退格*键)
-   .esc
-   .space
-   .up
-   .down
-   .left
-   .right

这些按键修饰符也可以组合使用，或和鼠标一起配合使用：

-   .ctrl
-   .alt
-   .shift
-   meta (Mac 下是 Command 键，Windows 下是窗口键)

例如：

```html
<!--ctrl+enter -->
<input @keyup.ctrl.enter="handle">

<!-- alt + click -->
<div @click.alt="handle">...</div>
```
#### 修饰符的串联

修饰符可以串联：

`<a @click.stop.prevent="handle"></a>`