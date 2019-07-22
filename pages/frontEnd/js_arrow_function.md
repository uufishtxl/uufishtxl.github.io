---
# layout: note_tutorial
title: Arrow function expression
catalog: true
tags: 
  - javascript
  - function expression
permalink: js_arrow_function.html
folder: frontEnd
summary: A syntactically compact alternative to a regular function expression
# sidebar: frontEnd_sidebar
# topnav: topnav
---

> Arrow function expressions are ill suited as methods, and they cannot be used as constructors.

In the old days, we define a function like this:

```
function addNums(num1, num2) {
  console.log(num1 + num2);
}
// expected printout: NaN, means not a number, given that we didn't specify the values
```

Assign default values to parameters: 

```
function addNums(num1 = 1, num2 = 1) {
  console.log(num1 + num2);
}
// expected printout: 2; the function takes in the default values
```

Call-back:

```
function addNums (num1 = 1, num2 = 1) {
    return num1 + num2;
}

console.log(addNums(5,5));
// expected printout: 10
```

### Let arrow funtion come into play

```
const addNums = (num1 = 1, num2 = 1) => {
    return num1 + num2;
}
console.log(addNums(5,5));
```

It works, but you don't necessarily have to include the curly braces. Make it simple like this:

```
const addNums = (num1 = 1, num2 = 1) => console.log(num1 + num2);

addNums(5,5)
```

If you want to return the result, you don't even need the return keyword.

```
const addNums = (num1 = 1, num2 = 1) => num1 + num2;
console.log(addNums(5,5));
```
