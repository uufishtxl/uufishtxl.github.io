---
# layout: note_tutorial
title: Equals
catalog: true
tags: 
  - javascript
permalink: js_equals.html
folder: frontEnd
summary: Different equal expressions
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Equals

Double equal: check the string merely, regardless of its data type.

```
const x = '10';
if(x == 10) {
  console.log('x is 10')
}
```

```
const x = 10;
if(x == 10) {
  console.log('x is 10`)
}
```

They both fit into the true scenario.

Triple equal is much more strict. It takes the data type into account as well. So, in this case, `x = '10'` does not match the true statement.