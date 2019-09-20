---
title: 正则表达式
catalog: true
tags: 
  - javascript
permalink: js_reg_exp.html
folder: frontEnd
summary: 正则表达式
---

## 概念性关键点

-   本身是一门语言
-   不能单独使用，需要其他语言转换才能发挥它的作用
-   正则表达式本身是一个由特殊字符组成的一个由规则的字符串
-   正则表达式一般用于对其他字符串进行逻辑过滤（验证信息是否合法、替换字符、分割、搜索）

## 用途

1.  检查字符串的合法性
    1.  验证用户名（a-z, 0-9, 不能全是数字，不能全是字母）
    2.  验证邮箱格式（XXX@qq.com）
    3.  验证电话号码（11位数字）
    4.  验证身份证（18位）
    5.  验证QQ号码格式（5-12纯数字，第一位不能为0）；
2.  提取字符串中的信息
    1.  提取一条短信中的数字
    2.  提取文件名后缀
3.  替换字符串
    1.  替换字符串中的非法字符
    2.  对电话号码进行屏蔽
    3.  替换占位符“hello {{name}}”


## 定义

`var expression = /pattern/[flags]` 

```JS
var expression = /abc/;
```

或者

 `var expression = new RegExp('pattern'[, 'flags'])`

 ```JS
 var expression = new RegExp('9', 'i');
 ```

{% include note.html content="模式修饰符可以连着写。" %}

### 特殊的表示

`\\d`，`\d`代表0-9之间的数字，特殊字符用反斜杠。

## 正则表达式的测试方法

| 测试方式 | 返回结果 |
| ------------- | ---------- |
| `expression.test(string)` | 返回`true`或`false` |
| `expression.exec(string)` | 返回数组或`null` |

{% include note.html content="返回的数组含有检测到的子串，子串在母串中的索引值，检测的母串。" %}

一旦检测到子串，会立即返回数组。如果再运行一次同样的方法，会检测到第二次出现子串的索引值，以此类推。

```JS
var str = "...";

var result = expression.test(str);

console.log(result);
```

## 字符串的检测方法


