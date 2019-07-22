---
# layout: note_tutorial
title: Methods
catalog: true
tags: 
  - javascript
  - methods
permalink: js_methods.html
folder: frontEnd
summary: Some simple methods and how to nest methods
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Method and object

A method is basically a function that is associated with an object. It always comes along with parenthesis, for example:

```
console.log(s.toUpperCase());
```

## Simple Methods

### toUpperCase

Convert a string into upper cases

```
const s = 'Hello World';

console.log(s.toUpperCase());
```

### toLowerCase

Convert a string a lower cases

### substring

Get part from a string. Define parameters to specify the starting and the ending positions.

```
const s = 'Hello World!'
console.log(s.substring(0, 5));
```

### split

Split a string to several parts.

The following example doesn't really define the parameter. By default, the string is splitted into letters.

```
const s = 'Hello World!'
console.log(s.split(''));
```

Handy use case: Convert a tag list into an array: 

```
const = `technology, computers, it, code`
// Imposes splits when a comma is detected
console.log(tags.split(', '))
```

### push

Add a value to an array.

```
const fruits = ['apples', 'oranges', 'pears'];
fruits.push('mangos')
console.log(fruits);
```

This operation works better than the working on [const](#variables) alone since you don't have to necessarily figure out the count of elements within the target array.

### unshift

Add a value to the beginning of an array.

```
const fruits = ['apples', 'oranges', 'pears'];
fruits.unshift('strawberries')
console.log(fruits);
```

### pop

Take the last one off an array.
```
fruits.pop();
```

### isArray

Check to see if something is an array.

```
console.log(array.isArray(fruits));
```

### indexOf

Check out the index of an elements within the array.

```
console.log(fruits.indexOf('oranges'));
```

### Method: JSON.stringify()

> The `JSON.stringify()` method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

## Nesting Methods

```
const s = 'Hello World!'
console.log(s.substring(0, 5).toUpperCase());
```