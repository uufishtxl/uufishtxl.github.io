---
# layout: note_tutorial
title: Literals
catalog: true
tags: 
  - javascript
  - literals
permalink: js_literals.html
folder: frontEnd
summary: object literals and array literals, adding or extracting data
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Object literals

> A JavaScript object literal is a comma-separated list of name-value pairs wrapped in curly braces. 

```
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30,
    hobbies: ['music', 'movies', 'sports'],
    address: {
        steet: '50 main st',
        city: 'Boston',
        state: 'MA'
    }
}
```

### Object literals and json

> The object literal notation is not the same as the JavaScript Object Notation (JSON). ... In JSON the values can only be strings, numbers, arrays, true , false , null , or another (JSON) object. A function value (see "Methods" above) can not be assigned to a value in JSON.

### Extracting data

#### Approach A

```
console.log(person.hobbies[1]);
```

#### ES6 Destructuring assignment (解构赋值)

> Destructuring assignment is a cool feature that came along with ES6. Destructuring is a JavaScript expression that makes it possible to **unpack** values from arrays, or properties from objects, **into distinct variables**. ES6 destructuring assignment makes it easier to extract this data.

> The object and array literal expressions provide an easy way to create ad hoc packages of data.
> 
> ```
> var x = [1, 2, 3, 4, 5];
> ```
> 
> The destructuring assignment uses similar syntax, but on the left-hand side of the assignment to define what values to unpack from the sourced variable.

```
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30,
    hobbies: ['music', 'movies', 'sports'],
    address: {
        street: '50 main st',
        city: 'Boston',
        state: 'MA'
    }
}

const { firstName, lastName, address: {city} } = person;

console.log(city);
```

### Adding data into an object literal

```
person = {
  ...
}

person.email = 'johndoe@email.com'

console.log(person);
```

The printout also includes the email address.

## Array literals

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