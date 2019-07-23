---
# layout: note_tutorial
title: Declare variables
catalog: true
tags: 
  - javascript
permalink: js_variables.html
folder: frontEnd
summary: var, let and const
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Resources

### Video tutorial: JavaScript Crash Course

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/hdI2bqOjy3c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Variables

### `var`, `let` and `const`

In JavaScript, there're basically three ways to set variables. We have `var`, `let` and `const`. 

`var` comes into view from the beginning of JavaScript. But you won't really want to use it anymore now that we've got `let` and `const`, because `var` is globally scoped, while `let` and `const` has block-level scopes.

With `let`, you can reassign values. `const` stands for *constant*, which means its value cannot be reassigned.

Using `const` allows you to add values to arrays. You can manipulate it, you can use methods on it. The only thing you can't do is to take the array and reassign it.

```
const fruits = ['apples', 'oranges', 'pears']
fruits[3] = 'grapes';
console.log(fruits);
```

The console prints out grapes as well. This, however, is not the best practice to add a value into an array. See [push](/js_methods.html#push) for a more refined solution.

Only use `const` unless you know you're going to reassign the value.