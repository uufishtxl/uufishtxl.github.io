---
# layout: note_tutorial
title: Looping
catalog: true
tags: 
  - javascript
  - looping
permalink: js_looping.html
folder: frontEnd
summary: For loop, while loop, looping and high order array methods
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Looping

### Array instance

```
const todos = [
    {
        id: 1,
        text: 'Take out of trash',
        isCompleted: true
    },
    {
        id: 2,
        text: 'Meeting with boss',
        isCompleted: true
    },
    {
        id: 3,
        text: 'Dentist appt',
        isCompleted: false
    }
];
```

### For loop

```
for(let i = 0; i < 10; i++) {
  console.log(`For Loop Number: ${i}`);
}
```

### While loop

While looping sets the variables outside of the loops.

```
let i = 0;
while(i < 10) {
  console.log(`While Loop Number: ${i}`);
  i++;
}
```

### Loop through an array

A traditonal way to do this:

```
for(let i = 0; i < todos.length; i++) {
    console.log(todos[i].text);
}

```

### A much more readable solution

Nonetheless, there's a much more readable solution.

```
// 'todo' is just a name; name it anything you like
for(let todo of todos){
  console.log(todo.text);
}
```

See? Dropping the `i` variable, this expression is way more graceful.

### High order array methods

Recommended for any kind of iteration with arrays.

#### `forEach()`

> `forEach()` **calls a provided `callback` function once for each element in any array** in ascending order. It is not invoked for index properties that have been deleted or are uninitialized (i.e. on sparse arrays).

```
todos.forEach(function(todo) {
    console.log(todo.text);
});
```

#### `map()`

> The map() method creates a new array with the results of calling a provided function on every element in the calling array.  
> 
> ```
> var array1 = [1, 4, 9, 16];
> 
> // pass a function to map
> const map1 = array1.map(x => x * 2);
> 
> console.log(map1);
> // expected output: Array [2, 8, 18, 32]
> ```

With map method, it returns an array. Here, we like to loop through the array literal and return an array of just the text values.

```
const todoText = todos.filter(function(todo) {
    return todo.text;
});

console.log(todoText);
```

#### `filter()`

Wield the `filter()` method to extract completed tasks:

```
const todoCompleted = todos.filter(function(todo) {
    return todo.isCompleted === true;
});

console.log(todoCompleted);
```

Employ the `map()` method in conjection with the `filter()` method to list the title of all completed tasks:

```
const todoCompletedText = todos.filter(function(todo) {
    return todo.isCompleted === true;
}).map(function(todo) {
    return todo.text;
});

console.log(todoCompletedText);
```