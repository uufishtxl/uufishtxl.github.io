---
title: vue-cli脚手架和项目初始化
catalog: true
tags: 
  - vue
permalink: vue_cli.html
folder: vue
summary: 安装脚手架并基于webpack创建项目
---

## 脚手架搭建

### 准备工作

-   安装 `Node.js`：官网下载系统对应的安装包
-   安装 `cnpm`

    ```
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    ```

### cnpm 和 npm 的区别

`npm`: node package manager, 包管理器。**弊端**：从国外服务器下载，可能出现异常。

`cnpm`: 淘宝团队完成的npmjs.org的镜像，避免安装Node.js时因为网络异常导致无法下载的问题。

安装`cnpm`：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### 安装 `vue-cli` 脚手架

安装，完成后查看版本。

```
cnpm install vue-cli -g

vue --version 
```

## 创建项目

通过vue创建一个基于webpack模板的新项目。

```
vue init webpack my-app
```

`Install vue-router?`，项目用到路由，当然选`Y`。

`Use ESLint to lint your code?`，ESLint 是代码的管理工具，统一代码风格。选Y，可能会对单引号、双引号、结束分号比较严格。希望警告，选`Y`，不希望，选`N`。

基本都选推荐选项和`Y`。

等待创建完成。

安装完成后，进入项目所在文件夹，以启动服务。

```
cd my-app
npm run dev
```

打开`vscode`，打开项目所在文件夹，即可正式开始建立项目。

### 报错的情况

一般归咎于某个package没有安装成功。找到相关安装包的名称，执行`cnpm install packageName`，即可。




