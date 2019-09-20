---
title: 基本概念
catalog: true
tags: 
  - javascript
permalink: js_note.html
folder: frontEnd
summary: JavaScript Basics
---


| Day | Segments | Learned |
| --- | -------- | ------- |
| 01 | 001 - 027 | √ |
| 02 | 028 - 052 | √ |
| 03 | 053 - 069 | √ |
| 04 | 070 - 088 | √ |
| 05 | 089 - 103 | √ |
| 06 | 104 - 127 | √ |
| 07 | 128 - 150 | × |
| 08 | 151 - 170 | × |
| 09-10 | 171 - 191 | ×× |




## 重点：JavaScript的引入方式


1.  内嵌式
2.  外链式：JS的外链方式用`src`属性，而不是`href`属性（`href`属性用在`a`标签和`link`标签中）
3.  在HTML标签中事件属性中引入  
    ```html
    <div 事件属性="JavaScript代码"></div>
    ```  
    比如：  
    ```html
    <div onclick="alert('1111')"></div>
    ```
4.  在a标签中href属性值中写入  
    ```html
    <a href="javascript:JS代码">点击弹出对话框</a>
    ```  
    ```html
    <a href="javascript:alert('2222')">点击弹出对话框</a>
    ```

## `console.log()`

可以输出多个变量，用逗号隔开

## 基本概念

### 语法 > 标识符 Identifier

就是指变量、函数、属性的名字。

-   第一个字符必须是一个字母、下划线或者一个美元符号
-   其他字符可以是字母、下划线、美元符号或数字

### 关键字和保留字

见《JavaScript 高级程序设计》，跳转到40页。

### 重点：变量

ECMAScript的变量是松散类型的。所谓松散类型，就是可以用来保存任何类型的数据。

每个变量仅仅是一个用于保存值的占位符而已。定义变量时要使用var操作符。
未经过初始化的变量，会保存一个特殊的值，undefined。

在函数中定义变量，这个变量在函数退出后会被销毁。

### 重点：数据类型

-   Undefined
-   Null
-   Boolean
-   Number
-   String
-   Object

#### typeof 操作符

检测给定变量的数据类型，可能返回下列某个字符串：

-   'undefined': 如果这个值未定义
-   'boolean'
-   'string'
-   'number'
-   'object'：如果这个值是对象，或是null，这其实就是JS的一个bug（这么理解，null是空对象，所以数据类型就是对象）
-   'function'


typeof是操作符，而不是函数，因此操作数并不需要包含在括号中。

#### Undefined类型

Undefined类型只有一个值，即特殊的undefined。

```JavaScript
var message
alert (message == undefined); // true
```

[阮一峰关于null和undefined的博客文章](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)

#### Null类型

```JavaScript
var car = null;
alert(typeof car); // 'object'
```

实际上，undefined值是派生自null值的。因此ECMA-262规定对它们的相等性测试要返回true：

```JavaScript
alert(null == undefined); // true
```

尽管`null`和`undefined`有这样的关系，但是它们的用途完全不同。无论在什么情况下，都没有必要把一个变量的值显式地设置为undefined，可是同样的规则对`null`却不适用。换句话说，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存null值。这样做不仅可以体现null作为**空对象指针**的惯例，而且也有助于进一步区分null和undefined。

#### `null`和`undefined`的比较

相同点：均代表无值

不同点：undefined代表一个变量没有赋值，null代表一个变量存储的值是引用类型，但是目前对象还没有创建，另外如果一个函数应该有返回值，但是最终没有数据作为返回值，那么也会返回`null`，总而言之，null表示一个空对象

#### Boolean

要将一个值转换为其对应的Boolean值，可以调用转换类型函数`Boolean()`。

可以对任何数据类型的值调用`Boolean()`函数，而且总会返回一个Boolean值，至于返回的这个值是true还是false，取决于要转换值的类型以及实际的值。

除了0 "" '' undefined NaN null得到false，其他都是true

```JavaScript
console.log(Boolean(" ")) // =>true
```


#### 数值

##### 浮点数值

该数值中必须包含一个小数点，并且小数点后面必须至少有一位数。
对于那些极大或极小的数值，可以用e 表示法（即科学计数法）表示的浮点数值表示。

##### 数值范围

由于内存的限制，ECMAScript 并不能保存世界上所有的数值。要想确定一个数值是不是有穷的（换句话说，是不是位于最
小和最大的数值之间），可以使用isFinite()函数。

##### NaN

NaN = Not a Number

用isNaN()函数来确定这个参数是否“不是数值”。`"10"`，这样的String以及布林值的`true`和`false`都会转换为数值，因此在下面的例子中，返回的值都是`false`。

```JavaScript
alert(isNaN(NaN)); //true
alert(isNaN(10)); //false（10 是一个数值）
alert(isNaN("10")); //false（可以被转换成数值10）
alert(isNaN("blue")); //true（不能转换成数值）
alert(isNaN(true)); //false（可以被转换成数值1）
```

`isNaN()`甚至适用于Object。在基于对象调用`isNaN()`函数时，会首先调用对象的valueOf()方法，然后确定该方法返回的值是否可以转换为数值。如果不能，则基于这个返回值再调用toString()方法，再测试返回值。

#### 数值转换

-   `Number()` 转型函数，适用于任何数据类型
    -   如果是Boolean值，`true`和`false`分别将被转换为1和0
    -   如果是`null`，返回0
    -   如果是`undefined`，返回`NaN`
    -   如果是字符串：
        -   字符串中只包含数字：将其转换为十进制数值 (011会变成11)
        -   字符串中包含有效的浮点格式，转换为对应的浮点数值
        -   字符串中包含有效的十六进制格式，将其转换为相同大小的十进制整数值
        -   字符串是空的，转换为0；
        -   字符串中包含上述格式之外的字符，转换为 `NaN`
    `Number()`函数转换比较复杂，不够合理，在处理整数时，更常用的是`parseInt()`函数。
-   `parseInt()`，专门用于把字符串转换成数值：`parseInt()`在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符。如果第一个字符不是数字字符或者负号，`parseInt()`就会返回`NaN`，而`Number()`对空字符返回0。如果第一个字符是数字字符，`parseInt()`会继续解析第二个字符，直至解析完所有后续字符或者遇到了一个非数字字符。比如说，`parseInt('1234blue') // 1234`，`parseInt('22.5') // 22`      
    转换八进制，比如“070”时，ES3和ES5存在分歧。解决方法是为这个函数提供第二个参数：转换时使用的基数（即n进制的n）。比如`var num = parseInt('0xAF', 16)`。
-   `parseFloat()`，专门用于把字符串转换成数值，与`parseInt()`类似。`parseFloat()`只解析十进制值，因此它没有用第二个参数指定基数的用法。

#### String类型

注意点：在输出的内容中如果需要使用引号，请使用转移符号“\”。

```
console.log("这是一个\"漂亮\"的女孩")
```

##### 字符字面量

转义序列表示1个字符。任何字符串的长度都可以通过访问其`length`属性取得，比如`alert(text.length)`。

如果字符串中包含双字节字符，那么length属性可能不会精确地返回字符串中的字符数目。

##### 转换字符串

有两种方式，第一种是使用几乎每个值都有的`toString()`的方法，但是不适用于`null`和`undefined`类型。

多数情况下，不必传递参数。不过，在调用数值的toString()方法时，可以传递第一个参数：输出数值的基数。可以输出二进制、八进制、十六进制，乃至其他任意有效进制格式表示的字符串值。默认以十进制输出。

比如：

```
var num = 10;
alert(num.toString(2)) // 1010
```

在不知道要转换的值是不是`null`或者`undefined`的情况下，还可以使用转型函数`String()`，这个函数能够将任何类型的值转换为字符串。String()函数遵循下列规则：

-   如果值有`toString()`的方法，则调用该方法（没有参数），并返回相应的结果；
-   如果值是`null`，则返回"null"；
-   如果值是`undefined`，则返回"undefined"。

#### object 类型

创建Object类型的实例，并为其添加属性和（或）方法，就可以创建自定义对象。

```JavaScript
var o = new Object();
```

这个语法与Java中创建对象的语法相似；但在ECMAScript中，如果不给构造函数传递参数，则可以省略后面的那一对圆括号，也就是：

```JavaScript
var o = new Object;
```
Object的每个实例都具有下列属性和方法：

-   constructor: 构造函数，也就是上方例子中的`Object()`
-   `hasOwnProperty(*PropertyName*)`: 用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。作为参数的属性名（propertyName）必须以字符串的形式指定，比如`o.hasOwnProperty("name")`
-   `isPrototypeof(object)`: 用于检查传入的对象是否传入对象的原型
-   `propertyIsEnumerable(*propertyName*)`: 用于检查给定的属性是否能够使用for-in语句来枚举。
-   `toLocalString()`: 返回对象的字符串表示，该字符串与执行环境的地区对应
-   `toString()`: 返回对象的字符串表示
-   `valueOf()`: 返回对象的字符串、数值或布林值表示。通常与`toString()`方法的返回值相同。

### 操作符

-   算数操作符
-   位操作符
-   关系操作符
-   相等操作符

应用于对象时，相应的操作符通常会调用对象的`valueOf()`和(或)`toString()`方法。

#### 一元操作符

##### 递增和递减

-   递增和递减：前置型和后置型，也就是相对于要操作的变量的位置。

前置型和后置型有区别。

```JavaScript
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2 // 等于21
var num4 = num1 + num2 // 等于21
```

```JavaScript
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2 //等于22
var num4 = num1 + num2 //等于21
```

**这是因为执行前置递减操作时，变量的值都是在语句被要求值以前改变的。后置则反之。**

在应用于不同的值时，递增和递减操作符遵循下列规则：

-   在应用于一个包含有效数字字符的字符串时，先将其转换为数字值，再执行加减1 的操作。字
符串变量变成数值变量。
-   在应用于一个不包含有效数字字符的字符串时，将变量的值设置为NaN。
字符串变量变成数值变量。
-   在应用于布尔值false 时，先将其转换为0 再执行加减1 的操作。布尔值变量变成数值变量。
-   在应用于布尔值true 时，先将其转换为1 再执行加减1 的操作。布尔值变量变成数值变量。
-   在应用于浮点数值时，执行加减1 的操作。
-   在应用于对象时，先调用对象的valueOf()方法以取得一个可供操作的
值。然后对该值应用前述规则。
    ```JavaScript
    var o = {
      valueOf: function() {
        return -1;
      }
    };

    o-- // 值变成-2
    ```

##### 一元加和减操作符

```JavaScript
var num = 25;
num = +num // 仍然是25
```

在对非数值应用一元操作符时，该操作符会像Number()转型函数一样，对这个执进行转换。

```JavaScript
var s1 = "01";

s1 = +s1 //值变成1
```

用于表示负数：

```JavaScript
var num = 25;
num = -num // 变成-25
```

#### 位操作符

按内存中表示数值的位来操作数值。

ECMAScript中所有数值都以IEEE-754 64位格式存储，但位操作符并不直接操作64位的值，而是先将64位的值转换成32位的整数，最后将结果转换为64位。

对于有符号的整数，32位中的前31位用于表示整数的值，第32位用于表示数值的符号，0表示正数，1表示负数。

负数同样以二进制码存储，但使用的格式是二进制补码，计算需要经过3个步骤：

1.  求这个数值绝对值的二进制码，比如要知道-18的二进制补码，就先要知道18的二进制码，也就是`0000 0000 0000 0000 0000 0000 0001 0010`
2.  求其二进制反码，也就是将0和1互换：`1111 1111 1111 1111 1111 1111 1110 1101`
3.  最后，二进制反码加1：`1111 1111 1111 1111 1111 1111 1110 1110`

但是ECMAScript会尽力向我们隐藏这些信息，换句话说，在以二进制字符串形式输出一个负数时，我们看到只是这个负数绝对值的二进制码前面加上了一个负号

```JavaScript
var num = -18;
alert(toString(2)) // "-10010"
```

#### 布尔操作符

-   非 (`NOT`)
-   与 (`AND`)
-   或 (`OR`)

##### 逻辑非

由一个叹号 (!) 表示，可以应用于ECMAScript中的任何值。无论这个值是什么数据类型，这个操作符都会返回一个布尔值。

-   如果操作数是一个对象，返回`false`
-   如果操作数是一个空字符串，返回`true`
-   如果操作数是一个非空字符串，返回`false`
-   如果操作数是数值0，返回`true`
-   如果操作数是任意非0的数值（包括Infinity），返回`false`
-   如果操作数是`null`，返回`true`
-   如果操作数是`NaN`，返回`true`
-   如果操作数是`undefined`，返回`true`

##### 逻辑与

逻辑与操作符由两个和好(`&&`)表示，有两个操作数，比如：

```JavaScript
var result = true && false
```

| 第一个操作数 | 第二个操作数 | 结果 |
| ------------- | ----------| ------------- |
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false

逻辑与操作可以应用于任何类型的操作数，而不仅仅是布尔值。

```JavaScript
var a = 1 && 2 // =>2 如果a为true，直接返回b，而不管b为true或者false。如果a为false，那么就直接返回a

var a=2,b=undefined,c=3;
var d = 2&&b&&c;
console.log(d) // =>undefined，不是布尔值
```

#### 逻辑或

a || b 如果a为false，则直接返回b的值，而不管b为true或者false。如果a为true，直接返回a，而不会继续往下执行

#### 相等操作符

相等和不相等——先转换再比较，全等和不全等——仅比较而不转换。

#### 字符串连接符号

a + b: 如果a和b中至少有一个字符串，此时 + 不是运算符加号，而是连接符，且得到的结果是字符串类型。

#### 赋值运算

必须是`a+=b`，不能是`a=+b`，比如`a=+30`中的`+`只是正号的意思。

#### 运算符优先级

不用记住，知道怎么查就可以。

`===`和`!==` `==` `!=`


## 变量

多个变量的声明：一个var直接声明多个变量，用逗号隔开。通常把带有赋值的变量放在最后。

`var a,b,c = 12` 并不是说a，b，c三个变量都赋值12，而是只有c有赋值。


##输出对话框

prompt('提示信息', 默认值)

-   输入框：根据提示要输入的信息
-   确定
-   取消：得到的是空对象

**注意**： `prompt`中的默认值是可选值，但是考虑到兼容性的问题，最好写上。

```JavaScript
var msg = prompt("您的年龄是：", 12);

console.log(msg, typeof msg); // 得到输入的值或者默认的值，值的类型为String；取消的话，得到的是null，类型是object
```
## 流程控制

`{}`只是为了包含代码块，如果只有一行需要执行的语句，完全可以去掉大括号。

```JavaScript
if(age >= 18) console.log("恭喜你，终于成年了！")
```

## 流程控制

分支判断最后的`else`可以省略。

### swith...case...

语法结构：

switch(判断谁的值) {
  case 值 A：
  执行的代码块 A
  break;

  case 值 B：
  执行的代码块 B
  break;

  case 值 C：
  执行的代码块 C
  break;

  ...

  default:
  执行代码块D
} 

注意事项：switch...case...语句既判断值的大小，也判断数据类型。

```JavaScript
var a = prompt('请输入1-10之间的整数', 1);

a = parseInt(a);

switch(a) {
  case 1:
  console.log("春天");
  break;

  case 2:
  console.log("夏天");
  break;

  case 3:
  console.log("秋天");
  break;

  case 4:
  console.log("冬天");
  break

  default: 
  console.log("不在四季中");
}
```

-   break的作用是：防止向后穿透代码块，强制跳出。

-   `default`相当于`if...else...`中的`else`，所以和`else`一样，可以省略。

-   `default`的位置可以变化。但是如果不在最后，必须加上break。

`switch...case...`和`if...else...`的区别：

`if...else...`可以判断值的大小，也可以判断值的范围，而`switch...case...`语句一般只判断值的大小。

## 循环语句

### for 循环

语法结构：

for(定义变量保存初始值；循环条件；更新循环次数) {

}

### while 循环

语法结构：

初始化循环变量
while(循环条件) {
  循环体;
  更新循环变量;
}

### do...while...循环

语法结构：

初始化循环变量
do{
  循环体
  更新循环变量
}while(循环条件);

### 死循环

循环条件永远为真，有两种情况：

-   没有循环条件，默认就为真
-   for(;;)

### 嵌套循环

语法结构：
for(外层循环) { // 外层循环相当于表格中的行
  for(内层循环) { // 内层循环相当于表格中的列

  }
}

```JavaScript
for(i = 0; i < 5; i++) {
            for (j = 0; j < 5; j++) {
                document.write('*');
            }
            document.write('<br>')
        }
```

输出到网页的结果：

```
*****  
*****  
*****  
*****  
*****
```  

#### 不规则的行和列

找规律（i和j之间的规律）。

```JavaScript
for (i = 4; i >= 0; i--) {
                for (j = 0; j < i + 1; j++) {
                    document.write('☆');
                }
                document.write('<br>');
            }
```

输出的效果：

☆☆☆☆☆  
☆☆☆☆  
☆☆☆  
☆☆  
☆  


### 终止循环

break：强制跳出当前循环  
  **注意*： 在没有指明跳出具体是哪个循环时，默认跳出当前循环  

```JavaScript
parentLoop: for (var i = 1; i <= 5; i++) {
    childLoop: for (var j = 1; j <= 5; j++) {
        if (j == 3) {
            break; // end up the child loop and continue with the parent loop
        }
        document.write('*');
    }
    document.write('<br>')
}
```
指定的情况：

```JavaScript
parentLoop: for (var i = 1; i <= 5; i++) {
  childLoop: for (var j = 1; j <= 5; j++) {
      if (j == 3) {
          break parentLoop; // end up the parent loop altogether
      }
      document.write('*');
  }
  document.write('<br>')
}
```
        
continue：终止本次循环，继续下次循环

因为跳出了父级循环，所以连父级循环中的换行符都省略去了。

```JavaScript
parentLoop: for (var i = 1; i <= 5; i++) {
    childLoop: for (var j = 1; j <= 5; j++) {
        if (j == 3) {
            continue parentLoop// end up the child loop and continue with the parent loop
        }
        document.write('*');
    }
    document.write('<br>')
}
```

输出效果：

**********

#### 跳出多层循环

## 函数

L53-L69：递归函数难度高，可以慢慢掌握

函数其实就是对一段代码进行封装，被封装的代码总是完成某项功能，函数不会主动地进行，需要在程序中手动地调用函数（比如：用户点击的时候），并且可以多次调用这个函数。

### 为什么使用函数

-   减少代码冗余
-   方便后期对代码的维护  

### 函数的定义

两种定义方式：

-   函数声明式
-   函数表达式

#### 函数声明式

function 函数名() {
  函数体（被封装的代码块）
}

#### 函数表达式

var 变量 = function() {
  函数体（被封装的代码块）
}

注意：
-   function(){} 匿名函数（没有名称的函数）
-   变量名相当于函数名

```JavaScript
// Encapsulation
var sayHello = function () {
            console.log('Hello World')
        };

// Run the function
sayHello();
```

#### 两种函数定义的区别

**函数声明式可以在定义前调用函数，而函数表达式则不可以。**

**如果使用函数声明式来定义函数，定义好的函数会自动提升位置，提升到`script`开始标签的开始位置。**

### 函数的命名规则

不能使用简单字符，要言之有意。

函数也是一种数据类型，属于引用类型。所以把函数赋值给一个变量是可行的。


### 形参和实参

调用函数时传入的实参和形参是一一对应的关系。

### 带返回值的函数

函数执行后的结果有可能被其它程序调用或者参与其它程序的运算，这时候需要返回值

function 函数名(参数1,参数2,...参数n) {
  return 函数执行后的结果;
}

### 三元运算符

a?b:c

### 带有返回值的函数

不管函数中有多少个返回值，函数执行的结果是第一次遇到的return的结果。简单地说，函数第一次遇到return，就结束。

### 变量的作用域

```JS
var a = 12;

function sum() {
  console.log(a);
  var a = 34;
  console.log(a);
}

sum();
```

正如函数声明式会提升到`<script>`开始位置类似，函数中变量的定义也会被提升到函数的起始位置，比如上方第一次出现的`console.log(a)`会输出`undefined`，就是因为函数a的定义被提升到了函数的开始位置，缺少赋值，因此输出为`undefined`。程序会以下面的方式进行解读：

```JS
var a = 12;

function sum() {
  var a;
  console.log(a);
  a = 34;
  console.log(a);
}

function sum()
```

### 内置函数

也叫做系统函数，比如`String()`, `Number()`, `Boolean()`, `parseInt()`, `parseFloat()`等

`isNaN`，判定是否为非数值。如果不是数字，返回true，如果是数字，返回false

### 递归函数

在函数体内对函数自身的调用

-   前提：
    -   必须是一个函数
    -   必须要有一个递归出口（对函数中的参数进行判断）
        参数必须满足一定的条件，才调用函数自身。

递归函数怎么写？

1.  第一步：假设递归函数已经写好  
    第n项的值：function f(n) {}  
    前n项的和：function fsum(n) {}  
2.  寻找递进关系  
    第n项的值的递进关系：  
    f(1) = 1;  
    f(2) = f(1) + 2;  
    f(3) = f(2) + 2;  
    ...  
    f(n) = f(n-1) + 2;  
    前n项的和的递进关系：  
    fsum(1) = 1;  
    fsum(2) = fsum(1) + f(2);  
    fsum(3) = fsum(2) + f(3);  
    ...  
    fsum(n) = fsum(n-1) + f(n)  
3.  将地推关系添加到假设好的递归函数中，形成递归体：  
    ```JS
    // f(n)
    function f(n) {
      return f(n-1) + 2;
    }
    // fsum(n)
    function fsum(n) {
      return fsum(n-1) + f(n);
    }
    ```
4.  寻找递归出口（临界条件）   
    ```JS
    // 第n项的值的临界条件
    if(n==1) {
      return 1;
    }
    // 前n项的和的临界条件
    if(n==1) {
      return 1;
    }
    ```
5.  进行拼装  
    ```JS
    function f(n) {
      if (n == 1) {
          return 1
      }
      return f(n - 1) + 2;
    }
    function fsum(n) {
    if (n == 1) {
        return 1
    }
    return fsum(n - 1) + f(n);
}
    ```

## 数组

数组是一组数据有序排列的集合。将一组数据按一定顺序组织为一个组合，并对这个组合命名，这样便构成了数组。

### 数组的定义

-   使用 new 字符实例化定义数组
    ```JS
    var arr = new Array();
    ```

-   使用字面量的方式定义数组 ----> 字面量：常量（固定数据）
    ```JS
    var arr = [/*...*/];
    ```

使用`new`定义的数组，如果数组中只写了一个数字，那么这个数字代表的是数组的长度，而不是数组元素。

`var arr = new Array(3);`

使用索引赋值时，通常以最大的索引为最后一个元素。

```JS
var arr3 = [];
arr3[0] = "number";
arr3[1] = "string";
arr3[12] = "boolean";
arr3["name"] = "undefined";
arr3[0] = "null";
console.log(arr3);
console.log(arr3.length);
```

### 栈区和堆

内存分为两个区域：

-   栈区： 用于存放
    -   基本数据类型的值
    -   引用类型的地址

-   堆：用于存放数据大小不固定的元素，包括数组和对象。

### 数组中元素的操作

#### 删除：`delete 数组名[索引]`

```JS
delete arr[1];
```

但是，删除后，数组长度并没有变化，被删除的数组元素为空，它的值是`undefined`替代。

#### 清空数组

-   直接将数组重新赋值为空数组 `arr = []`  
-   或者也可以将数组的长度设置为0 `arr.length = 0`

#### 修改数组

就是对数组中的元素重新赋值。

```JS
arr[1] = "number";
```

0 <= 索引 <= 数组的长度 - 1

#### 添加数组元素

索引 >= 数组的长度

### 数组的遍历

-   使用`for`循环遍历
-   使用for...in...遍历 `for(变量 in 数组名)` 不过这里的变量是索引值，而不是数组中的元素

#### 两种遍历方式的区别

-   使用`for`循环遍历数组（**推荐使用**）：
    -   `for`循环中的i值数据类型为`number`
    -   把数组中所有的值都遍历出来（包括不存在的值，比如说用`delete`删除的值）
-   使用`for in`循环遍历数组：
    -   for...in中k值的数组类型为`String`
    -   只遍历数组中存在的值（就是指具体数据的值），这种方式通常被称为枚举

### 二维数组

以数组作为数组元素的数组

字面量方式很简单:

```JS
var arr = [
  [1,2,3],
  ['number', 'string'],
  ['张三','李四']
];
```

下面是new字符定义数组：

```JS
var arr = new Array(
  new Array(1, 2, 3),
  new  Array('number', 'string'),
  new Array('张三', '李四')
);
```

另外，还有第三种方式：先定义好多个一维数组，再将这些数组作为数组元素添加到一个一维数组中。

```JS
var arr1 = [1,2,3];
var arr2 = ['number', 'string'];
var arr3 = ['张三','李四'];

varr arr4 = [arr1, arr2, arr3];
```

访问二位数组中元素的方法

`arr[x][y]`

#### 向二维数组中添加元素

和一维数组一个道理。

### 数组自身的常用方法

 #### `Array.prototype.concat()`

 连接两个或更多的数组，并返回结果。

 ```JS
 var arr
    
var arr1 = [1, 3, 5];

var arr2 = ["smith", "job", "white"];

var arr3 = ["a", "b", "c"];

var arr = arr1.concat(arr2, arr3);

    console.log(arr); // 输出为一个数组[1, 3, 5, "smith", "job", "white", "a", "b", "c"]
 ```

#### `Array.prototype.join()`

把数组中所有元素按指定的分隔符分割，放入一个字符串

```JS
var arr = ["smith", "white"];

var fullName = arr.join(' '); // 如果没有传值，默认用逗号分割

console.log(fullName); // 输出smith white
```

#### `Array.prototype.pop()`

删除并返回数组中的最后一个元素。

```JS
var arr = ["a", "b", "c", "d"];

var popValue = arr.pop();

console.log(arr, popValue); // 原数组被删除元素。该方法返回的是被删除的元素

```

#### `Array.prototype.shift()`

删除并返回数组中的第一个元素。

```JS
var arr = ["a", "b", "c", "d"]; 

elem = arr.shift();

console.log(arr, elem); // 原数组变成["b", "c", "d"]。该方法返回的是被删除的元素
```

#### `Array.prototype.push()

向数组的末尾添加一个或多个元素，并返回数组的长度。

```JS
var arr = ["a", "b", "c", "d"];

var newArr = arr.push("e", "f");

console.log(arr, newArr); // 原数组变成["a", "b", "c", "d", "e", "f"]。该方法返回的是数组当前的长度
```

#### `Array.prototype.unshift()`

向数组的起始位置添加一个或多个元素，并返回数组的长度。

```JS
var arr = ["a", "b", "c", "d"];

var newArr = arr.unshift(1, 2);

console.log(arr, newArr); // 原数组变成[1, 2, "a", "b", "c", "d"]。该方法返回的是数组当前的长度
```

#### `Array.prototype.reverse()`

将原数组元素逆序排列

```JS
var arr = ["e", "b", "c", "d"];

arr.reverse();

console.log(arr); // 原数组变成["d", "c", "b", "e"]
```

#### `Array.prototype.slice(start, end)`

arr.slice(开始的位置, 结束的位置)，可从已有数组中返回选定的元素。

注意：slice方法是左闭右开，所以能取到开始位置的元素，而不能取到结束位置的元素。结束位置是可选的，如果没有，表示从开始位置到结束。

```JS
var arr = ["a", "b", "c", "d"];

newArr = arr.slice(1, 2);

console.log(arr, newArr); // 原数组不变，该方法会返回新数组，显示"b"（遵循左闭右开的规则）

```

#### `Array.prototype.sort()`

规定排序顺序，原数组会被替换。

```JS
var arr = [13, 9, 10, 34];

function compareNum (a, b) {
    return a-b; // a-b 按照从小到大的顺序排列，b-a按照从大到小的顺序排列
}

arr.sort(compareNum);

console.log(arr);// 显示[13, 9, 10, 34]
```

#### `Array.prototype.splice()`

`Array.prototype.splice(删除开始位置,删除多少个元素,在删除位置新增的元素A,在删除位置新增的元素B等等)`

-   删除开始位置：必须有 
-   删除多少个元素：如果不想删除，只想添加，传入0 `arr.splice(2, 0, "newEleA", "newEleB")`
-   新增的元素：可选


```JS
var arr = ["红楼梦", "西游记", "水浒传", "三国演义"];

arr.splice(1, 2, "曹雪芹", "罗贯中");

console.log(arr); // 原数组被替换，变成了["红楼梦", "曹雪芹", "罗贯中", "三国演义"]
```

#### 选择排序：`Array.prototype.()`



#### 冒泡排序：`Array.prototype.()`


## 对象

### 内置对象

-   String：字符串对象
-   Math：数学对象
-   Number：数字对象
-   Date：日期对象
-   BOM：浏览器对象模型，操作浏览器（了解即可）
-   DOM：文档对象模型，操作文档

### 自定义对象

自己定义的对象。

定义对象的两种方式

-   第一种方式：使用`new`字符来实例化对象 `new Object()`
-   第二种方式：使用字面量的方式定义对象 `var obj = {}`

#### 给对象添加属性和方法

-   第一种方式：通过对象来添加 `object.attribute = value`
-   第二种方式：


#### 方法中的`this`

`this`表示调用该方法的对象


### 字符串对象的方法

#### `string.length`

字符串对象的长度

#### `string.charAt(索引值)`

返回在指定索引值位置的字符。

索引超出，返回空字符串

```JS
var str1 = "note";

var letter = str1.charAt(5);

console.log(letter); // 索引超出 为空字符串

var charType = typeof(letter); // 类型为String


console.log(charType)
```

#### `string.indexOf()`

返回某个指定的字符串值在字符串中**首次**出现的位置。

`string.indexOf(searchvalue, fromindex)`

searchvalue可以是多个字符。

```JS
var name = "this is a box";

var aLetter = name.indexOf("s");

console.log(`第一个s是第${aLetter + 1}个字母`) // 是索引值哦，所以真正的位置要+1

var zLetter = name.indexOf("z");

console.log(zLetter); // 返回-1，不存在的字符串总是返回-1
```

#### `string.lastIndexOf()`

查找字符串值最后一次出现的位置

```JS
var str = "this is a box. that's is a Box";

var is = str.lastIndexOf("is");

console.log(is) // 22
```

#### `string.replace(regexp/substr, replacement)`

用新字符去替换既有字符。

`string.replace(既有字符，新字符)`

```JS
var str = "this is a box. that's is a Box";

newStr = str.replace("is", "**"); // string.replace方法并不会改变原字符串，而是返回一个新的字符串
console.log(newStr); // 默认只替换了第一个匹配值

// 如果要替换所有匹配值，需要使用正则

strAll = str.replace(/is/g, "**" ) // g: global

console.log(strAll);
```

#### `string.substr()`

`substr`没有使用驼峰命名法。

`string.substr(从指定的索引值开始截取字符串, 截取多少个字符)`

```JS
var str = "this is a box. that's is a Box";

var subStr = str.substr(2, 5); // 如果起始位置超过了字符串长度，返回空字符串。

console.log(subStr);
```

#### `string.substring()`

`string.substring(从什么位置开始截取，截取到什么位置)`

注意，和`string.substr()`不一样。

另外，还有一点很重要，截取的范围是一个左闭右开的区间。

```JS
var str = "this is a box. that's is a Box";

var subString = str.substring(2, 5); // 如果未定义结束位置，将截取到最后

console.log(subString); // 这次，返回的是is (is后面还有个空格)
```

#### `string.toLowerCase`

#### `string.toUpperCase`


### Number 对象

`toFixed()`

四舍五入为指定小数位数的数字。

### Math 对象

#### `Math.PI`

```JS
console.log(Math.PI); // 返回π值`
```

#### `Math.abs(x)`

返回数x的绝对值

```JS
Math.abs(-1) // 返回1
```

#### `Math.ceil(x)`

对一个数x向上取整数。

```JS
Math.ceil(3.4) // 返回4
```

#### `Math.floor(x)`

对一个数x向上取整数。

```JS
Math.floor(3.4) // 返回3
```

#### `Math.max(x)`

求最大值。

```JS
Math.max(Math.PI, 1, -3)
```

#### `Math.min(x)`

求最小值。

`Math.pow(x,y)`

返回x的y次幂值

Math.pow(2, 3) // 8

`Math.random()`

返回介于0到2之间的一个随机数，包含0不包含1。

`Math.round(x)`

可以把一个数字舍入为最接近的整数。

```JS
Math.round(3.6);
```

#### 获取指定范围的随机整数

### Date 对象

#### `new Date()`

获取当前计算机时间。

#### `new Date(dateVal)`

获取给定时间。


#### 时间差

#### 获取年月日等具体信息

```js
// 在页面中显示时间: 2017-3-30 18:03:46星期四

var localTime = new Date();
console.log(localTime);

// 获取年

year = localTime.getFullYear();

console.log(year);

var month = localTime.getMonth();

var day = localTime.getDate(); // 不是getDay()，getDay是返回一周中的某一天

var weekday = localTime.getDay();// 完全可以理解成为索引值

var hour = localTime.getHours();

var min = localTime.getMinutes();

var sec = localTime.getSeconds();

var week = ['星期日','星期一','星期二','星期三','星期四','星期五','星期六']; //将weekday作为索引值去遍历这个数组，就能获取中文的weekday信息

weedayCn = week[weekday];

var str = `${year}-${month + 1}-${day} ${hour}:${min}:${sec}${weedayCn}` // 月份需要+1

console.log(str);*/

```

#### 将时间转换为字符串

```JS
var mydate = new Date();

// 转换为字符串

mydate = mydate.toLocaleString();

console.log(mydate);

```

## JS的组成

-   ECMAScript: js基本语法、函数、数组和对象  
    ES5 (2018年1月还是主流) ES6 (2015年发布) ES7(还存在兼容性问题)
-   DOM (Document Object Model)，主要操作的是HTML标签，使JavaScript有能力与HTML文档的所有元素“对话”
-   BOM (Browser Object Model)，主要操作的是浏览器窗口，使JavaScript有能力与浏览器“对话”  
    -   操作浏览器窗口
    -   访问浏览器历史

BOM 和 DOM 是独立于程序语言和平台的标准，W3C定义了一组标准接口，而这些接口在浏览器中以对象的形式实现。BOM与DOM均由一组对象组成，对象定义了**属性**和**方法**。

**注意**： 

-   BOM 和 DOM 只是一个概念 (一个模型)，而不是具体的对象，它们是由多个对象组成的集合。
-   `window`对象中有个属性是`document`，`document`又是一个对象 --- 就是 DOM 对象模型。

### BOM

BOM 对象的结构：

1.  BOM对象中最顶层的对象是`window`对象
2.  window对象中有很多属性，这些属性少数又是一个对象
    -   window.document：DOM对象模型
    -   window.history：历史对象
    -   window.location：地址对象
    -   window.navigator：导航对象
    -   windows.screen：屏幕对象
    -   frames[]：框架对象

### window 对象

window对象是脚本中的全局对象，可以在任何地方调用。

1.  window对象：全局对象（可以省略不写）  
    window.alert() 简写成 alert();
2.  window全局对象中的属性：全局属性（全局变量）
    **注意**：在外部定义的变量和函数，其实就是全局对象中的属性和方法。

### window对象中的方法

#### `alert()`

略

#### `confirm()`

显示带有一段消息以及确认按钮以及取消按钮的对话框。点击不同的按钮返回不同的值

-   确定按钮：`true`
-   取消按钮：`false`

可以用if语句一起使用，实现控制。

```JS
var a = confirm("确定要删除文件吗？");

if(a) {
    ...
} else {
    ...
}
```

#### 计时器

-   间歇调用：每隔多少毫秒调用代码块：
    -   第一种写法：`setInterval(function, interval)`，比如`setInterval((){}, 500)`，例子中的函数是匿名函数。
    -   第二种写法：可以把匿名函数调出来，然后传入函数名，比如说`funciton 函数名() {}`，然后`setInterval(函数名, 500)` 。注意，函数名的话，后面不跟括号哦。
-   超时调用：经过若干秒只调用一次代码块。  
    语法：`setTimeout(function, interval)`，同样有两种写法，和间歇调用类似

**注意**：推荐使用间歇调用。

##### 清除计时器

`clearInterval(间歇调用ID号)`

每创建一个计时器，就会自动赋予一个ID号。

`cleearTimeout(超时调用ID号)`

### BOM 中的其他对象

#### screen 对象

`window.screen`

#### history 对象

-   `length`属性：表示当前打开的浏览器历史列中的URL数。

-   `back()`：访问上一个页面：`history.back()`

-   `forward()`：访问下一个页面 `history.forward()`

-   `go(1)`：参数可正可负，跳到指定页面 `history.go(-2)`，就是跳到上上个页面。

#### location 对象

操作地址栏。

地址的组成部分：

-   protocol：协议
-   hash: 表示URL地址中的锚点部分，包括前导符#。
-   host：表示主机名（hostname）和端口号（port），即IP地址或者域名端口。
-   pathname：页面路径，包含页面文件名称
-   search：参数部分
-   href：所有地址 (`location.href`，获取当前页面的地址)，可读可写。`location.href="https://www.youtube.com"`

#### 练习：若干秒后跳转页面

```HTML
<head>
  ...
  <style>
    * {
        background-color: #000;
        color: #fff;
        line-height: 40px;
        text-align: center;
    }
  </style>
</head>
<body>
  <p><span id="sec"></span> 秒后将跳转到 www.baidu.com</p>
</body>
```

```JS
var n = 5;
document.getElementById('sec').innerHTML = n;

setInterval(function() {
    n--;
    if (n===0) {
        location.href="https://www.baidu.com";
    } else {
        document.getElementById('sec').innerHTML = n;
    }
}, 1000)
```

#### navigator 对象

包含了浏览器的所有信息。

`navigator.userAgent`返回客户机发送给服务器的user-agent头部的值，可以使用它来判断打开当前文件的是什么浏览器（是chrome，firefox还是ie）

## DOM 文档对象

-   核心DOM：用于XML与HTML的共用接口（方法），可以用来操作节点数，

-   XML DOM（不用掌握）：用于专门操作XML

-   HTML DOM：针对标签中的属性进行操作（修改属性、获取属性的值）。

### HTML 节点数

通过节点数得到的结论：

1.  整个文档就是一个节点：文档节点 - document
2.  而每个HTML标签就是一个元素节点
3.  标签中的文字则是文字节点
4.  标签中的属性则是属性节点
5.  一切都是节点。

### 获取元素的方法

DOM：操作网页的内容，包括：

-   标签
-   标签中的属性
-   css样式属性
-   标签中的内容

有几种方法：

-   通过id获取元素（标签）  
    语法结构：  
      `document.getElementById("ID名")`
    **注意**：id在页面中是唯一的。所以通过id获取的元素只有一个。
-   通过标签名获取
    语法结构：
      `document.getElementsByTagName("标签名称")`
    **注意**：通过标签名获取的结果是一个数组 | 获取某个范围A内的元素B： 1. 先获取该范围A； 2. 再到A下面获取元素B | 获取到的数组不能直接使用，必须要精确到其中的元素才能使用

-   通过类名获取元素
    语法结构：
      `document.getElementsByClassName("类名")`
    **注意**：这种获取方式在IE9下不兼容

-   通过Name属性值获取：一般针对表单中的空间（input select textarea button）
    语法结构：
      `document.getElementByName("name值")` >> 只能使用document
    **注意**：这个结构只能在`document`下面获取

#### 快速访问方式 (了解)

通过`name`属性快速访问元素，主要针对表单。存在兼容性问题，一般不使用，了解即可。

```JS
myformObj = document.myform;
console.log(myformObj);
```

```JS
myformObj = document.myform;
// 通过name属性快速访问input框
sex1 = myformObj.sex1;
console.log(myformObj);
console.log(sex1)
```

#### HTML5快速访问

兼容高版本的浏览器。

`document.querySelector("选择器")` // 返回页面中的第一个元素

`document.querySelectorAll("选择器")` // 返回页面中所有匹配的元素

选择器：

-   id名：#id
-   类名：.类名
-   标签名：标签名


console.debug(): 专门用来打印对象

元素对象中的属性：HTML标记的属性（标签属性）对应于元素对象的一个同名属性。

通过元素对象中的同名属性进行访问和修改。

### 获取属性

对象.属性名

### 表单对象中的属性

属性：

-   length: 表示表单中控件(input textarea button select)的个数 （不包含label）
-   elements: 访问表单中的所有控件的一个数组

  
### 表单对象中的方法

`onsubmit`：在提交表单之前调用，如果onsubmit，返回true，则提交表单，返回false，则阻止表单提交。

注意：

-   在提交表单之前触发，验证用户信息是否正确。正确就提交，错误则不提交。
-   如果函数没有返回值，默认返回true

书写位置：在表单标签中作为标签属性添加。


### 阻止浏览器的默认行为


### `onreset`

在表单被重置前调用。如果onreset返回true，则重置表单，返回false则组织表单重置。

同样绑定在表单上。

### submit()

form对象上的提交方法。

注意：普通按钮是不能直接提交的，可以通过添加点击事件来触发表单提交。

#### 文本对象

获取input框。

像disabled这种二选一的状态值，用js来设置属性值得时候统一用Boolean值。

checked：单选和复选框的选中

selected：下拉框的选中

readOnly

设置标签属性时：

-   `disabled = "disabled"`
-   `disabled`

## 第七天：节点操作

### 获取根节点

### 









