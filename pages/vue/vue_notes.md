---
title: Vue.js P1
catalog: true
tags: 
  - vue
permalink: vue_note_p1.html
folder: vue
summary: 梁灏 《Vue.js》 实战笔记
---

## `el`

```html
<div id="app"></div>
var app = new Vue ({
  el: document.getElementById('app') // 或者是#app
})
```

`el`: 用于指定一个页面中已存在的 DOM 元素来挂载 Vue 实例，可以是 HTML Element，也可以是 CSS 选择器。挂载成功后，可以通过`app.$el`来访问该元素。

## 数据绑定

`v-model`的值对应于创建的 Vue 实例的 `data` 选项中的 `name` 字段，这就是 Vue 的数据绑定。通过 Vue 实例的 `data` 选项，可以声明应用内需要双向绑定的数据。Vue 实例本身也代理了 `data` 对象里的所有属性，所以可以这样访问。

```JavaScript
var app = new Vue ({
  el: '#app',
  data: {
    a: 2
  }
})

console.log(app.a); // 2
```

除了显示地声明数据外，也可以指向一个已有的变量，并且它们之间默认建立了双向绑定，当修改其中任意一个时，另一个也会起变化。

```JavaScript
var myData = {
  a: 1
}

var app = new Vue ({
  el: '#app',
  data: myData
})

console.log(app.a) // 2

app.a = 2;
console.log(myData.a) // 2

myData.a = 3;
console.log(app.a) // 3
```

## Vue 的生命周期

与 `JQuery` 的 `ready()`方法相似。

```JavaScript
$(document).ready(function() {
  // DOM 加载完成后，会执行这里的代码
  ...
});
```

Vue 的生命周期钩子与之类似。比较常用都有：

`created` 实例创建完成后调用，此阶段完成了数据的观测，但尚未挂载，`$el`尚不可用。需要初始化处理一些数据会用到。

`mounted` `el`挂载到实例上后调用，第一个业务逻辑会在这里开始。

`beforeDestroy` 实例销毁之前调用。主要解绑一些使用 `addEventListener` 监听的事件等。

这些钩子与 `el` 和 `data` 类似，也是作为选项写入 Vue 实例内，并且钩子的 `this` 指向的调用它的 Vue 实例。


## `<v-html>`

输出 `html`，而不是纯文本。

```html
<div id = "app">
  <span v-html = "link"></span>
</div>

<script>
  var app = new Vue({
    data: {
      link:'<a href="#">链接</a>'
    }
  })
</script>
```

## {% raw %} {{}} {% endraw %}

### 文本插值

```html
<h1>{{ title }}</h1>
```

### 显示文本插值的标签

在元素标签上加上`v-pre`。

```html
<span v-pre>{% raw %} {{这里的内容不会被编译}} {% endraw %}</span>
```

### 简单运算和三元运算

```html
<div>
{% raw %}
  {{ number * 2 }}
  {{ isComplete ? '完成' : '未完成' }}
  {{  text.splite(',').reverse().join(',')}}
{% endraw %}
</div>
```

{% include note.html content="Vue.js 只支持单个表达式，不支持语句和流控制。在表达式中，不能使用用户自定义的全局变量，只能使用 Vue 白名单内的全局变量，例如 Math 和 Date。" %}

## 过滤器

支持在文本插值的尾部添加一个管道符 “ \| ”，经常用于文本的格式化，比如：

-   字母全部大写
-   数字加入千位符
-   时间的格式化

还是用刚才的时间显示做例子。

```html
<!-- formatDate 是一个自定义的用于过滤的函数 写入 Vue 的filters选项中 -->
{% raw %}{{ date | formatDate }}{% endraw %} 
```

```JavaScript
<script>
  var padDate = function(value) {
    return value < 10 ? '0' + value : value;
  }
  export default {
    ...,
    filters: {
      formatDate = function(value) {
        var date = new date(value); // value是指位于管道符前需要过滤的数据
        var year = date.getFullYear();
        var month = padDate(date.getMonth() + 1);
        var day = padDate(date.getDate());
        var hours = padDate(date.getHours());
        var minutes = padDate(date.getMonths());
        var seconds = padDate(date.getSeconds());
        return year + '-' + month + '-' + 'day' + ' ' + hours + ' : ' + minutes + ' : ' + seconds;
      }
    }
  }
</script>
```

### 过滤器的串联

```
{% raw %}{{ message | filterA | filterB }}{%  endraw %}
```

### 接收参数

```
{% raw %} {{ message | filterA('arg1', 'arg2') }} {% endraw %}
```

{% include note.html content="过滤器用于简单的文本转换，如果要实现更为复杂的数据变化，应该使用计算属性。" %}

## 指令与事件

指令的**主要职责**：当其表达式的值改变时，相应地将某些行为应用到 DOM 上。

```html
<div id="app">
  <!-- show的值为true时，才会显示p元素 -->
  <p v-if="show">显示这段文本</p> 
</div>
```

***数据驱动 DOM 是 Vue.js 的核心理念***，因此，不到万不得已，不要自行主动操作 DOM，只需要维护好数据，Vue 会优雅地帮忙处理 DOM 的改动。

### `v-bind`

用于动态更新 ***HTML 元素上的属性***，比如`id`、`class`等。

```html
<div id="app">
  <a v-bind:href="url">链接</a>
</div>

<script>
  var app = new Vue({
    el: '#app',
    data: {
      url: 'https://www.baidu.com'
    }
  })
</script>
```

### `v-on`

绑定事件的监听器。

```html
<div id="app">
  <p v-if="show">这是文本</p>
  <button v-on:click="handleClose">点击隐藏</button>
</div>

<script>
  var app = new Vue({
    el: '#app',
    data: {
      show: true
    },
    methods: {
      handleClose: function() {
        this.show = false;
      }
    }
  })
</script>
```

除了`click`外，还有`dbclick`、`keyup`、`mousemove`等。表达式可以是

-   一个方法名，这些方法都写在Vue实例的`methods`属性内，并且是函数的形式，函数内的 `this`指向的是当前 Vue 实例本身，因此可以直接用this.xxx的形式来访问或修改数据，如实例中的 `this.show = false`；

-   也可以直接是一个内联语句

    ```html
    <div id="app">
      <p v-if="show">这是文本</p>
      <button v-on:click="show = false">按钮</button>
    </div>
    ```

Vue.js 将 `methods` 里的方法也代理了，所以可以像访问 Vue 那样来调用方法。

## 语法糖

不影响功能的情况下，添加某种方法实现同样的效果，从而方便程序开发。

`v-bind`和`v-on`都提供了语法糖，也可以说是缩写:

-   `v-bind`可以省略直接写成一个冒号

    ```html
    <a :href="url">链接</a>
    ```

-   `v-on`可以直接用@来缩写
    ```html
    <button @click="handleClose">按钮</button>
    ```



