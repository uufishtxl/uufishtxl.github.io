---
title: 表单与 v-model
catalog: true
tags: 
  - vue
permalink: vue_v_model_basics.html
folder: vue
summary: 基本用法
---

`v-model` 指令：用于在表类元素上双向绑定数据。比方说，在输入框上使用时，输入的内容会实时映射到**绑定的数据**上。

-   使用`v-model`后，表单控件显示的值只依赖所绑定的数据，不再关心初始化时的`value`属性，对于在`<textarea></textarea>`中插入的值，也不会生效
-   输入中文时，在输入拼音阶段不会触发更新。如果想要这么做的话，可以用@input来替换`v-model`
-   `v-model`是一个特殊的语法糖，只不过会在不同的表单上进行智能化的处理

[基本知识、单选按钮和复选框的相关示例](https://jsfiddle.net/edith_tang/qnLfv70p/68/)

## 单选按钮

-   单独使用：不需要使用`v-model`，直接绑定一个布尔类型的值即可。（***问题***：这个修改选中状态还要另外绑定方法？好像是只能从未选中变成选中的状态，然后就不可逆了）

-   互相排斥的一组单选按钮：需要使用`v-model`配合`value`来使用。一旦选中，v-model绑定的数据的指就会变成选中选项的`value`属性。

[基本知识、单选按钮和复选框的相关示例](https://jsfiddle.net/edith_tang/qnLfv70p/68/)

## 复选框

-   单独使用：

-   组合使用：将多个`checkbox`使用`v-model`绑定到同一个`Array`类型的数据。当某个复选框的`checked`状态为`true`时，它的`value`属性值就会被`push`到这个数组中。

[基本知识、单选按钮和复选框的相关示例](https://jsfiddle.net/edith_tang/qnLfv70p/68/)

## 选择列表

[选择列表相关示例](https://jsfiddle.net/edith_tang/wrv2dmtp/32/)

选择列表，也就是下拉选择器。

### 单选场景

单选的场景：

1.  v-model绑定一个String类型的数据

2.  选中后，会优先匹配选中项的value值，如果没有value值，则会去匹配option的text。

3.  会在初始化后忽视option本身的selected属性

4.  当绑定的数据的初始值就是某个选项的value值时，初始化后会默认选中改选项

### 多选场景

选择列表多选的场景：

1. 在`<select>`标签上添加`multiple`属性，即可变成多选列表

2. 和复选框一样，用`v-model`会绑定一个Array类型的数据

3. 选中选项会，会将它匹配（优先匹配`value`，次则`<option>`的text）并push到Array数据中

### 利用`data`和`v-for`来对`<options>`元素进行渲染

1.  在业务中，`<option>`经常用`v-for`动态输出，value和text也是用v-bind来动态输出的

2.  虽然在`<select>`中可以简单地完成下拉选择需求，但是在实际业务中反而不常用。因为它的样式依赖平台和浏览器，无法统一，也不美观，功能也受限（比如，不支持搜索），所以常见的解决方案是用`<div>`模拟一个类似的控件。具体可以在学习了组件（components）的内容后再进行尝试。


## 自定义组件

从 Vue.js 2.x 开始，`v-model`还可以用于自定义组件，满足定制化需求，在后面章节开始介绍。