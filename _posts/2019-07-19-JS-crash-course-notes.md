---
layout: post
title: JavaScript Crash Course
subtitle: Sass Crash Course Summary
date: 2019-07-19
author: edith
header-img: "img/bg_web_design2.jpg"
catalog: true
tags: 
  - javascript
  - webpage_design
---

## Resources

### Video tutorial: JavaScript Crash Course

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/hdI2bqOjy3c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Variables

### `var`, `let` and `const`

In JavaScript, there're basically three ways to set variables. We have `var`, `let` and `const`. 

`var` comes into view from the beginning of JavaScript. But you won't really want to use it anymore now that we've got `let` and `const`, because `var` is globally scoped, while `let` and `const` has block-level scopes.

With `let`, you can reassign values. `const` stands for constant, which means its value cannot be reassigned.

Using `const` allows you to add values to arrays. You can manipulate it, you can use methods on it. The only thing you can't do is to take the array and reassign it.

```
const fruits = ['apples', 'oranges', 'pears']
fruits[3] = 'grapes';
console.log(fruits);
```

The console prints out grapes as well. This, however, is not the best practice to add a value into an array. See [push](#push) for a more refined solution.

Only use `const` unless you know you're going to reassign the value.

## Simplification

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

## Methods

### Method and object

A method is basically a function that is associated with an object. It always comes along with parenthesis, for example:

```
console.log(s.toUpperCase());
```

### Simple Methods

#### toUpperCase

Convert a string into upper cases

```
const s = 'Hello World';

console.log(s.toUpperCase());
```

#### toLowerCase

Convert a string a lower cases

#### substring

Get part from a string. Define parameters to specify the starting and the ending positions.

```
const s = 'Hello World!'
console.log(s.substring(0, 5));
```

#### split

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

#### push

Add a value to an array.

```
const fruits = ['apples', 'oranges', 'pears'];
fruits.push('mangos')
console.log(fruits);
```

This operation works better than the working on [const](#variables) alone since you don't have to necessarily figure out the count of elements within the target array.

#### unshift

Add a value to the beginning of an array.

```
const fruits = ['apples', 'oranges', 'pears'];
fruits.unshift('strawberries')
console.log(fruits);
```

#### pop

Take the last one off an array.
```
fruits.pop();
```

#### isArray

Check to see if something is an array.

```
console.log(array.isArray(fruits));
```

#### indexOf

Check out the index of an elements within the array.

```
console.log(fruits.indexOf('oranges'));
```

#### Method: JSON.stringify()

> The `JSON.stringify()` method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

### Nesting Methods

```
const s = 'Hello World!'
console.log(s.substring(0, 5).toUpperCase());
```

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

### Array literal

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

## Looping

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

#### Traditonal practice

A traditonal way to do this:

```
for(let i = 0; i < todos.length; i++) {
    console.log(todos[i].text);
}

```

#### A much more readable solution

Nonetheless, there's a much more readable solution.

```
// 'todo' is just a name. Name it anything you like
for(let todo of todos){
  console.log(todo.text);
}
```

See? Dropping the `i` variable, this expression is way more graceful.

#### High order array methods

Recommended for any kind of itemration with arrays.

> `forEach()` **calls a provided `callback` function once for each element  in any array** in ascending order. It is not invoked for index properties that have been deleted or are uninitialized (i.e. on sparse arrays).

```
todos.forEach(function(todo) {
    console.log(todo.text);
});
```

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

## Condition

### if statement

#### `||`: is or

```
const x = 6;
const y = 11;
if(x > 5 || y > 10) {
console.log('x is more than 5 or y is greater than 10');
};
```

#### `&&`: is and

```
const x = 6;
const y = 11;
if(x > 5 && y > 10) {
    console.log('x is more than 5 and y is greater than 10');
}
```

This is much more efficient than nesting if statements within another if expression.

#### `?` is then, `:` else

```
const x = 10;

const color = x > 10 ? 'red' : 'blue';

console.log(color)
```

### Switches

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

## Arrow functions

In the old days, we define a function like this:

```
function addNums(num1, num2){
  console.log(num1 + num2);
}
// expected printout: NaN, means not a number, given that we didn't specify the values
```

```
function addNums(num1 = 1, num2 = 1){
  console.log(num1 + num2);
}
// expected printout: 2; the function takes in the default values
```

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

## About OOP

OOP, also known as object-oriented programming

### Class

> It is the design or blurprint of any entity, which defines the core properties and functions.

### Inheritance

> In OOP, the meaning of inheritance is very close to its actual meaning in English.
> 
> ![inheritance](/img/oop_inheritance.png)

### Object

> An object is an inheritance of a class which has physical existence.
> 
> My name is *edith*, and I am an *object* of class *Female*.
> 
> HumanBeing, Male or Female, we just mean a type/kind.
> 
> You, me, our friends, have physical existence, while class is just a logical definition.

### Abstraction

> Abstraction means hiding the details from the outside world.

### Encapsulation

> Encapsulation refers to binding properties with functions.

### Polymorphism

> Polymorphism means "many forms". It allows us to define more than one way to do something., either by using a different proces sfor it or by using different parts to do it.
> 
> Polymorphism methods:
> 
> -   Overriding: Everyone walks in the direction of his face. If one walks while facing the other direction, this is overriding. When you change the mechanism of function, it is called "overriding"
> -   Overloading: When we use our hands, not our legs, to walk, overloading occurs.
>     ```
>     class HumanBeing:
>         def walk(hands):
>             print "Walk using our hands"
>             print "this is overloading"
>     ```

-   **class**: HumanBeing

    -   **Properties**: Body Parts
        -   Hands
        -   Legs
        -   Eyes...
    -   **Functions**: Body functions:
        -   Walk()
        -   Talk()
        -   See()

## Termiology


| Term | Explanation | Example |
| High-level | there's a lot of abstraction | JavaScript is a high-level, interpreted programming language.|