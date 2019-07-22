---
# layout: note_tutorial
title: Control flow
catalog: true
tags: 
  - javascript
permalink: js_control_flow.html
folder: frontEnd
summary: if statement, conditions and switches
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## if statement

### `||`: is or

```
const x = 6;
const y = 11;
if(x > 5 || y > 10) {
console.log('x is more than 5 or y is greater than 10');
};
```

### `&&`: is and

```
const x = 6;
const y = 11;
if(x > 5 && y > 10) {
    console.log('x is more than 5 and y is greater than 10');
}
```

This is much more efficient than nesting if statements within another if expression.

### `?` is then, `:` else

```
const x = 10;

const color = x > 10 ? 'red' : 'blue';

console.log(color)
```

## Switches

Route judgment into different directions (cases) and thus produce disparate results.

keywords: `case`, `break`, `default`

```
const x = 10;

const color = x > 10 ? 'red' : 'blue';

switch(color) {
    case 'red':
        console.log('color is red');
        break;
    case 'blue':
        console.log('color is blue');
        break;
    default: 
        console.log('color is not red or blue');
}
```