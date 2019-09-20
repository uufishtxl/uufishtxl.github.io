---
title: 初步认识项目文件夹
catalog: true
tags: 
  - vue
permalink: vue_files_folders.html
folder: vue
summary: 初步认识项目文件夹中的内容
---

-   `build`：webpack的相关配置信息
-   `config`：整个项目核心的配置文件
-   `node_modules`：项目的依赖包。打包时可以删除或者ignore。建议用DOS命令删除。
-   `src`：整个项目的模块。
    -   `main.js`：入口文件
    -   `App.vue`入口的组件
    -   `router`：对应的路由
    -   `components`：组件
    -   `assets`：静态资源，图片、字体图标、css等
-   `static`：全局的静态资源，与`src`文件不同的是，打包的时候会直接拷贝，不会改变路径。
-   `test`：测试相关
-   `.babellrc`: bable
-   `package.json`: 配置文件


## `main.js`

`Vue.config.productionTip = false` 阻止生产模式的一些消息

`#el: '#ele'` 挂载元素

## `router > index.js`

路由配置信息：

```JS
...
export default new Router({
  routes: [
    {
      path: "/", // 路径
      name: 'HelloWorld', // 路由的名字
      component: HelloWorld // 要加载的组件
    }
  ]
})
```

### 关于@

@ 前往 build > webpack.base.conf.js，就能看到@配置的是什么