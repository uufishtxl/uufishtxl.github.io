---
title: 组件详解
catalog: true
tags: 
  - vue
permalink: vue_components_slot.html
folder: vue
summary: 使用 slot 发布内容
---

什么时候需要用到 slot？

*When to use `slot`?*

当需要混合使用父组件内容和子组件模板时，就会用到 slot。这个过程叫作**内容发布 (<b data-toggle="tooltip" data-original-title="{{site.data.vue_dict.transclusion}}">`transclusion`</b>)**。有两个特点：

*`slot` is a handy touch when a father component should accommodate content of its own and child component templates in promiscuity*. Such process is called ***transclusion***. You should note its two features as below:

-   The father component, say, `<app>`, has no clue as to what content would be mounted in it. The decision is his father's.

-   Chances are `<app>` has its own template as well.

`<slot>` element serving as distribution outlets for content.



## About Compilation Scope

`slot` has access to the same instance properties, that is to say, the same "scope" as the rest of the template. That it to say, The slot in `<app>` does not have access to `<my-component>`'s scope.

## `slot` 的用法

可以在子组件开启一个插槽 (`slot`)。在父组件模板里，插入在子组件标签内的所有内容将替代子组件`<slot>标签及它的内容`。在父组件没有`slot`时，则会渲染子组件中`<slot>`中的内容。

[范例](https://jsfiddle.net/edith_tang/n4yxokrt/2/)

### 具名 `Slot` | Named slots

可能会需要多个 `Slot`，这时候可以给`<slot>`元素指定`name`属性，就可以分发多个内容。具名Slot可以和单个Slot共存。

打个比方，我在子组件上开了很多槽口，并且留了一个没有命名，其它都给了名字。然后我在父组件上定义元素的时，会在上面标明`slot`属性，也就是槽的名字，那这个元素就会被放到相应的槽口里面去进行渲染。

那那些没有`<slot>`属性的元素和内容就会被统一归类到默认的槽中。

如果没有默认的开槽，就直接将它们丢弃。

### 作用域插槽

[范例](https://codepen.io/uufishtxl/pen/abdEVar)

子组件的插槽上用类似props的写法绑定了数据。父组件使用`<template>`元素，而且拥有一个`scope="props`的特性，这里的`props`只是一个临时变量，就和`v-for="item in items"`中的`item`一样。这样，<template>标签就能通过临时变量`props`来访问子组件插槽的数据`msg`。

作用域插槽更具代表性的用例是列表组件。但是书中的例子显得多此一举，不过例子只是为了示范如果使用作用域插槽。

作用域插槽的使用场景是既可以复用子组件的`slot`，又可以使`slot`的内容不一致。

[范例](https://codepen.io/uufishtxl/pen/YzwYYKG)

分解步骤：

1.  将父组件的数据通过`props`传递给子组件。

2.  子组件在`props`选项中接收数据，并将它保存到一个自身的数据中。

3.  决定两个组件混用的元素，这里是`<li>`标签，所以在父组件中，在子组件的标签里插入`<li name="tab" scope="props">{{ props.tabName }}</li>`，这里，有几个注意点：

    a.  `name="tab"`指定目标插槽。  
    b.  `scope="props"`中的`props`是一个临时变量，就和`v-for="item in items"`中的`item`一个道理。  
    c.  `props.tabName`中的`tabName`还未定义，需要在子组件的`<slot>`中进行定义，作为props对象的属性。

4.  为了完成3-c步骤，需要在子组件的`<slot>`标签绑定自定义属性`<slot v-for="tab in tabList" :tabName="tab.name">`。

## 访问`slot`

访问被`slot`分发的内容的方法`$slot`，请看示例。

`$slot`在业务中几乎用不到，在用`render`函数创建组件时会比较有用。

{% include note.html content="书里的组件高级用法暂时跳过了" %}
