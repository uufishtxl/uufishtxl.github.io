---
title: 组件详解
catalog: true
tags: 
  - vue
permalink: vue_components_slot.html
folder: vue
summary: 其他
---

## `$nextTick`

### Vue.js 的更新 DOM 方式

在观察到数据变化后，Vue 不会马上就去更新 DOM。而是会开启一个队列，在缓冲时去检查并删除重复的数据，从而避免不必要的计算和 DOM 操作。然后，在下一个事件循环 tick 中，Vue 刷新队列并执行已经去重的工作。

也就是说，如果你用一个 for 循环来动态改变状态 100 次，其实 Vue 只会执行最后一次改变。如果不这么做，DOM 就会重建 100 次，无异是一个很大的开销。

这就是 Vue 异步更新队列的概念。

所以[范例]https://jsfiddle.net/edith_tang/7jfn8myL/4/()中，虽然已经执行了`showDix = true`，但是`div`仍然没有被创建出来，直到下一个 Vue 事件循环时，才开始创建。`$nextTick`就是用来知道什么时候 DOM 完成更新。

所以只要基于上面的例子，将获取文字所在`<div>`并将它打印出来的代码放入`this.$Tick(function() {})`中，就不会再次报错。

主要会在使用一些会去创建、更新及销毁完整生命周期的第三方库时，就需要利用好`$nextTick`。

## X-Templates

如果没有使用 `webpack`、`gulp`等工具，如果组件的`template`内容很长，写起来很不方便。

这时候，可以在`HTML`代码中使用<script type="text/x-template id='id-name'">来包围原来应该在`template`中的内容。然后再在注册组件时，使用`template = '#id-name'`来挂钩。

[范例](https://codepen.io/uufishtxl/pen/ZEQvxXR)

## 手动挂载实例

[https://codepen.io/uufishtxl/pen/KKVZooQ](https://codepen.io/uufishtxl/pen/KKVZooQ)

三种做法参考[范例](https://codepen.io/uufishtxl/pen/KKVZooQ)

手动挂载了解就好。

