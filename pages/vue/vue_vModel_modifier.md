---
title: 表单与 v-model
catalog: true
tags: 
  - vue
permalink: vue_v_model_modifier.html
folder: vue
summary: 绑定值
---

[这一节的代码范例](https://jsfiddle.net/edith_tang/aq9fkj7s/27/)

`v-model`的修饰符用来控制数据同步的机制。

## `.lazy`

在输入框中，`v-model`默认是在`input`事件中同步输入框的数据（除了特别说明过的中文输入法比较特殊外），使用修饰符`.lazy`会转变为在 `change` 事件中同步。以文本输入框为例，就是会在按下`ENTER`键或输入框失去焦点时，才会同步数据。


## `.number`

使用修饰符`.number`可以将输入转换为`Number`类型。这是考虑到即便是需要输入数字的输入框，输入内容绑定的数据也仍然是`String`类型，那利用这个修饰符，就能立即转换为`Number`数据类型。

## `.trim`

使用修饰符`.trim`可以去除输入内容的首尾空格。