---
# layout: note_tutorial
title: Concatenation
catalog: true
tags: 
  - javascript
permalink: js_concatenation.html
folder: frontEnd
summary: Wield template strings for simplifed concatenation
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Simplified concatenation

/kən'kætə'neʃən/ 

Traditional way of concatenation:

```
const name = 'John';
const age = 30;
console.log('my name is ' + name + ',' + ' and my age is ' + age);
```

### Template strings

> Template literals are string literals allowing embedded expression. 

```
const name = 'John';
const age = 30;
// Start your variable with a dollar sign and surround its name within curly braces.
const hello = `My name is ${name} and I am ${age}.`;
console.log(hello);
```