---
title: 绑定属性和内联样式
catalog: true
tags: 
  - vue
permalink: vue_note_directive_bind.html
folder: vue
summary: 梁灏 《Vue.js》 实战笔记
---

## 了解 `v-bind` 指令

## 绑定`class`的几种方式

### 对象语法

动态切换是否赋予`class`属性。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/ahd0Levy/10/)

也可以传入多个属性，来动态切换`class`，并且与静态`class`属性可以共存。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/ahd0Levy/15/)

当`:class`的表达式过长，还可以绑定一个计算属性。一般当条件多于两个时，都可以使用`data`或`computed`，例如使用计算属性：

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/507qzebu/12/)

除了计算属性，可以直接绑定一个`Object`类型的数据，或者使用类似计算属性的 `methods`。

### 数组语法

当需要多个`class`时，可以使用数组语法，给`:class`绑定一个数组，应用一个`class`列表。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/2wLthmfu/13/)

也可以使用三元表达式来根据条件切换`class`，例如：

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/2wLthmfu/12/)

样式error会始终应用，当数据`isActive`为`true`时，`active`样式才会应用。

上面的写法比较繁琐，可以在数组语法中使用对象语法。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/gctmx9ed/3/)

与对象语法一样，也可以使用`data`, `computed`, `methods`三种方法，以计算属性为例：

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/jnxm8qt4/12/)

{% include note.html content="上面的例子中，可以看到return的数组里的第二个`Object`类型的元素的key值用`[]`包围了起来，这是ES6的语法，为了确保key可以使用变量" %}


### 在组件上使用

需要`components`相关知识，先跳过，后面再补充。

## 绑定内联样式

`v-bind:style`或者`:style`，方法与`:class`类似，也有对象语法和数组语法，看起来很像直接在元素上写`css`。

[《Vue.js实战》中的例子](https://jsfiddle.net/edith_tang/qxrudeyh/2/)

{% include note.html content="CSS属性名称使用驼峰命名法 (camelCase)，或短横分隔命名法 (kebab-case)。" %}

大多数情况下，直接写一长串不便于阅读和维护，所以一般写在`data`或`computed`里。

应用多个样式对象时，可以使用数组语法：

`<div :style="[styleA, styleB]">文本</div>`

在实际业务中，绑定内联样式并不常用，因为往往可以写在同一个对象里面，较为常用的是计算属性。另外，使用`:style`时，会自动给特殊的CSS属性名称增加前缀，比如`transform`。










