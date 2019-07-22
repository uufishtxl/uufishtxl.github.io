---
# layout: note_tutorial
title: Literals
catalog: true
tags: 
  - javascript
  - literals
permalink: js_literals.html
folder: frontEnd
summary: var, let and const
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

### Extracting data - Approach A

```
console.log(person.hobbies[1]);
```

### Extracting data - ES6 Destructuring assignment (解构赋值)

> Destructuring assignment is a cool feature that came along with ES6. Destructuring is a JavaScript expression that makes it possible to **unpack** values from arrays, or properties from objects, **into distinct variables**. ES6 destructuring assignment makes it easier to extract this data.

```
const { firstName, lastName, address: { city } } = person;
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