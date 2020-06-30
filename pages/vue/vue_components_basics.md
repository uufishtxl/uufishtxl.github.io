---
title: 组件详解
catalog: true
tags: 
  - vue
permalink: vue_components_basics.html
folder: vue
summary: 组件与复用
---

[这一节的范例](https://jsfiddle.net/edith_tang/ervdwxnk/29/)

-   全局注册

-   局部注册：使用components选项可以局部注册组件，注册后的组件只有在该实例作用域下有小

全局注册后，任何 Vue 实例都可以使用。

全局注册示例代码如下：

```JavaScript
Vue.component('my-component', {
  // 选项
})
```
-   `my-component`: 自定义标签名称，推荐kebab的方式来命名
-   要在父级实例中使用组件，必须在实例创建前注册。[示例](https://jsfiddle.net/edith_tang/hyauzf2d/6/)  
    可能意思就是`Vue.component('component-name', {//选项})`要出现在建立父级组件的代码之前吧。
-   `Vue.component()`中的`template`选项必须包含且只能包含一个元素。

[示例](https://jsfiddle.net/edith_tang/hyauzf2d/9/)

### Vue 组件的模板受到的限制

-   `<table>`内规定只允许是`<tr>`、`<td>`、`<th>`等这些表格元素，所以在`<table>`内直接使用组件是无效的。这种情况下，可以使用特殊的`is`属性来挂载这些组件

-   另外常见的限制元素还有`<ul>`，`<ol>`，`<select>`。

{% include note.html content="如果使用的是字符串模板，就不会被限制。" %}

## `data`的特殊性

除了`template`外，组件还能包括其它选项：

-   `data`
-   `computed`
-   `methods`等等

但是在使用 `data`时，和实例有区别，`data`必须是函数，然后将数据 return 出去。

也可以return一个外部的对象。比如[下面的例子](https://jsfiddle.net/edith_tang/ervdwxnk/29/)。

`<quotation-external>`元素用了三次。当点击后，会发现按钮的名称会同步变化。这是因为这个组件引用的是外部的对象。JavaScript中对象是引用的关系。所以这个对象就是共享的，任何一方修改都会同步。

所以还是建议使用组件本身的数据，这样就不影响复用了。


