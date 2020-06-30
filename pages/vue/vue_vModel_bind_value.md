---
title: 表单与 v-model
catalog: true
tags: 
  - vue
permalink: vue_v_model_bind_value.html
folder: vue
summary: 绑定值
---

[这一节的代码范例](https://jsfiddle.net/edith_tang/aq9fkj7s/27/)

前面一节里，有提到单独使用单选按钮时，只需要绑定一个布尔值；组合使用时，则仅需使用`v-model`绑定一个String类型的数值，去匹配选中项的`value`或者`text`。

但是在实际开发中，有时候需要绑定一个动态的数据，这时可以使用`v-bind`来实现。

## 单选按钮

单选按钮，使用`v-model`绑定值。

选中时，`app.picked === app.value`，也就是123。

## 复选框


复选框，使用`v-model`绑定值。

选中时，`app.toggle`是`true-value`的值；未选中时，`app.toggle`是`false-value`的值。

{% include note.html content="toggle在书中的例子中默认是个布尔值，但是如果是布尔值，一开始就会显示是false了，我不知道是不是有别的说法，还是就是可以让它的初始值就是未选中状态时的值。" %}

## 选择列表

选中时，`app.selected`是一个`Object`，所以`app.selected.number  === 123`。如果用文本插值`{% raw %}{{ selected }}{% endraw %}`，渲染出来的就是`{% raw %}{{ "number": 123 }}{% endraw %}`

## 修饰符

`v-model`的修饰符用来控制数据同步的机制。

### `.lazy`

在输入框中，`v-model`默认是在`input`事件中同步输入框的数据（除了特别说明过的中文输入法比较特殊外），使用修饰符`.lazy`会转变为在 `change` 事件中同步。以文本输入框为例，就是会在按下`ENTER`键或输入框失去焦点时，才会同步数据。


### `.number`

使用修饰符`.number`可以将输入转换为`Number`类型。这是考虑到即便是需要输入数字的输入框，输入内容绑定的数据也仍然是`String`类型，那利用这个修饰符，就能立即转换为`Number`数据类型。

### `.trim`

使用修饰符`.trim`可以去除输入内容的首尾空格。

## 自定义组件

从 Vue.js 2.x 开始，`v-model`还可以用于自定义组件，满足定制化需求，在后面章节开始介绍。