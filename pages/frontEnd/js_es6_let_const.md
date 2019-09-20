---
title: ECMAScript 6
catalog: true
tags: 
  - javascript
permalink: js_es6_let_const.html
folder: frontEnd
summary: let const 和 var
---


# ES6

## 变量的声明

### var和let的比较

#### 作用域的不同

##### `for`循环作为佐证

##### 小知识：`for`循环中的两个作用域

#### “变量提升”的现象

#### TDZ (暂时性死区)

##### 对typeof 操作符的影响

#### let不允许在相同的作用域，重复声明一个变量

#### ES6允许浏览器有自己的行为方式

##### 函数声明类似于var 会提升到全局作用域、函数作用域的头部

##### 函数声明还会提升到所在块级作用域的头部

##### 避免在块级作用域声明函数，尽量使用表达式

### const

#### const一旦声明变量，就不得改变值

#### 声明的同时，必须立即初始化，不能之后再赋值

#### 和let一样，只在所在的代码的作用域内有效

#### 本质：实质上只能保证指向的内存地址不会，至于它的数据结构完全不能控制

### ES5：2种方式（var和function）

### ES5新增了四种，有 let, const, import和class

### 顶层对象的属性与全局变量

在ES5中，两者是相等的。
ES6改变了这一点 `let`命令 `const`命令 `class`命令声明的全局变量，不属于顶层对象的属性。

```
 var a = 1;

 console.log(window.a); // 1

 let b = 2;

 console.log(window.b); // undefined 用let命令声明的变量和顶层对象没有关系
 ```

#### 浏览器的顶级对象是window

#### Node中的顶级对象是global

#### 浏览器和Web Worker里，self也指向顶层对象，但是Node没有self

#### 同一段代码能够在各种环境，取到顶层对象，就要用this变量，但是它有局限性

## 变量的解构赋值
