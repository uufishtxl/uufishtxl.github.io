---
title: 组件详解
catalog: true
tags: 
  - vue
permalink: vue_components_props.html
folder: vue
summary: 使用 props 传递数据
---

## 基本用法

### `props`中声明的数据与`data`函数返回的数据的同异点

-   `props`来自父级，`data`是组件自己的数据，作用域是组件本身
-   都可以在模板`template`、计算属性`computed`及`methods`中使用


如果要传递多个数据，在`props`数组添加项即可。

#### kebab-case和camelCase的选择

HTML 的特性是不区分大小写，当使用 DOM 模板时，驼峰命名的 props 名称要转换成短横命名。

### 传递动态数据到子组件

[以文本输入框`<input type="text">`为例](https://jsfiddle.net/edith_tang/jxu8h74b/latest/)，需要做的事情是：

1.   在文本输入框用`v-model`将输入内容绑定到数据`favBook`。

2.   在父级的`<my-component>`标签上，将favBook的值绑定到一个自定义属性上，比如`:favorite="favBook"`。

3.   子组件的接收`props`，就完成了。

### 用`v-bind`传递`prop`

[示例](https://jsfiddle.net/edith_tang/43Lmwryj/12/)

如果要直接传递数字、布尔值、数组、对象，要使用`v-bind`来给子组件传递数据。所以为了避免混淆，即使传递字符串，建议也用`v-bind`。

## 单向数据流

Vue 1.x 中，通过props传递数据支持双向数据流。为了避免子组件无意中修改父组件的状态，需要尽可能将父子组件解耦，因此v2.x中只支持通过props来让父组件单向传递数据给子组件。

业务中，经常会碰到两种需要改变prop的情况。

1.  第一种做法是父组件传递prop到子组件，子组件将它作为初始值保存到自身的某个数据中，在自己的作用域下任意使用和修改。

2.  `prop`作为需要被改变的原始值保存到子组件的一个计算属性中。

[以上示例，请点击这里。](https://jsfiddle.net/edith_tang/kgj0um5y/16/)

{% include note.html content="在JavaScript中，对象和数组是引用类型，指向同一个内存空间，所以 props 是对象和数组时，在子组件内改变是会影响父组件的。" %}

上面这个Note提示我并不明白到底怎么回事 = =||||||

## 数据验证

之前的介绍里，`props`都是一个数组。但是当牵涉到数据验证时，`props`必须是对象。

[《Vue.js》中的范例](https://jsfiddle.net/edith_tang/a68uo4kh/5/)

验证的 `type` 类型有：

-   String

-   Number

-   Boolean

-   Object

-   Array

-   Function

`type`也可以是一个自定义构造器，使用`instanceof`检测。
