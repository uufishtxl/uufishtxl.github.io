---
title: svg-sprite-loader
catalog: true
tags: 
  - vue
  - webpack
  - svg
permalink: vue_svg_sprite_loader.html
folder: vue
summary: 如何使用`svg-sprite-loader`使用文字图标
---

### 简介

`svg sprite`有一个缺点，就是无法实现增量更新。这时候，我们就需要了解一下`svg-sprite-loader`。

`svg-sprite-loader`的工作原理是，通过某个文件夹来统一管理`svg`文件，然后通过`loader`将它们打包成`sprite`，这样，就实现了增量更新。如果想要新增图标，只需要将新加的`svg`文件放到对应的文件夹下就可以了。

### 安装

```
npm install svg-sprite-loader -D
```

### 配置

#### 示范文件夹

`D:\VUE\iconfont\iconfont`

找到`vue.config.js`文件。

```javascript
const path = require('path') // Node.js相关，path是Node.js的模块，用于路径处理

function resolve(dir) {
  return path.join(__dirname, './', dir); 
}

modules.exports = {
  chainWebpack: config => {
    config.module
      .rule('svg')
      .exclude.add(resolve('src/assets/icons'))
  }
}
```

### 参考知识

#### `path`模块相关

`path.join()`是`Node.js`中`path`模块的一个方法，可以将多个参数值字符串结合成一个路径字符串。该方法的主要用于在于，会正确使用当前系统的路径分隔符，`Unix`系统是“/”，`Windows`系统是“\”。

`__dirname`：当前文件的绝对路径。

### `chainWebpack`

#### `VUE CLI`

`vue cli`是一个官方发布`vue.js`项目脚手架，一个专门为单页面应用快捷搭建繁杂的脚手架，它可以轻松创建新的应用程序，而且可用于自动生成`vue`和`webpack`的项目模板。

`vue cli`会根据配置好的模板迅速搭建起一个项目工程来，省去自己配置`webpack`配置文件的基本内容。

####  `webpack`

`webpack`就是前端资源模块化管理和打包工具，可以将很多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源，还可以将按需加载的模块进行代码分割，等到实际需要的时候在异步加载。而要它实现这些功能，就需要提前编辑好配置文件。

#### `chainWebpack`

`vue cli`内部的`webpack`配置是通过`webpack chain`维护的。这个库提供了一个`webpack`原始配置的上层抽象，使其可以定义具名的`loader`规则和具名插件，并有机会在后期进入这些规则，并对它们进行修改。

它允许我们更细粒度地控制其内部配置。


#### `Rule.exclude`

排除所有符合条件的模块。

```js
config.module
  .rule('svg')
  .exclude.add(resolve('src/assets/icons'))
  .end()
```

#### `Rule.include`

引入符合以下任何条件的模块。

#### `Rule.loader`

是`Rule.use: [ { loader }]`的简写。

`Rule.use`可以是一个应用于模块的`UseEntries`数组。每个入口 (entry) 指定适用一个 loader。

#### `Rule.test`

引入所有通过断言测试的模块。





