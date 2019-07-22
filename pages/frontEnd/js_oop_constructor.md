---
# layout: note_tutorial
title: Object constructor function
catalog: true
tags: 
  - javascript
  - oop
permalink: js_oop_constructor_function.html
folder: frontEnd
summary: Class-based programming in JavaScript
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Constructor functions

1.  Start a function name with a capitalized letter, in this case, the **P** in *Person*.
2.  Pass in the properties you want to be able to set, `firstName, lastName, dob` here.
3.  Set as the properties of the object. We do that with `this`.
    Meaning `this.dob` equals the dob passed in.

```
// Constructor 
function Person(firstName, lastName, dob) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = dob;
}

// Instantiate object
const person1 = new Person('John', 'Doe', '4-3-1980');
const person2 = new Person('Marry', 'Smith', '3-6-1970');
console.log(person1)
console.log(person2.firstName);
```

The printout as a result of `console.log(person1)` is prefixed with the actual name of the object, which is `Person`.

### Taking a side route: Date constructor

Let's turn the date string into a date object using the date constructor.

```
//Constructor
function Person(firstName, lastName, dob) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = new Date(dob);
}

// Instantiate object
const person1 = new Person('John', 'Doe', '4-3-1980');
const person2 = new Person('Marry', 'Smith', '3-6-1970');

console.log(person1.dob);
console.log(person2.dob.getDate());
```

#### Creating a JavaScript date instance

> Creates a JavaScript Date instance that represents a single moment in time in a platform-independent format.

| `new Date()` | no parameters provided, <br/>so the date object represents the current date and time |
| `new Date(value)` | An integer value <br/>representing the number of milliseconds since January 1, 1970 00:00:00 UTC<br/> for example, `new Date(1563763956000)` |
| `new Date(datestring)` | A string value representing a date<br/>For example, `new Date('4-3-1980')` |

When you have a date object, there are a bunch of methods you can call on, such as `getDate`.

### Add methods into a class

Add methods which are basically just functions to this person object.

```
//Constructor
function Person(firstName, lastName, dob) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = new Date();
    this.getBirthYear = function() {
      return this.dob.getFullYear();
    }
    this.getFullName = function() {
        return `${this.firstName} ${this.lastName}`;
    }
  }
  
  //Intantiate object
  const person1 = new Person('John', 'Doe', '4-3-1980');
  
  console.log(person1.getBirthYear());
  console.log(person1.getFullName());
```

### Prototypes

Previously, we have created `class` using constructor functions. This, however, is not a perfect way in that properties and functions emerge side by side, like this:

![juxtapose](img/oop_juxtapose.png)

So we likely wish to put the functions under prototypes (using prototype methods), like this

```
//Constructor
function Person(firstName, lastName, dob) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = new Date();
  }

  Person.prototype.getBirthYear = function() {
    return this.dob.getFullYear;
  }

  Person.prototype.getFullName = function() {
      return `${this.firstName} ${this.lastName}`;
  }
  
  //Intantiate object
  const person1 = new Person('John', 'Doe', '4-3-1980');
  
  console.log(person1.getBirthYear());
  console.log(person1.getFullName());
  console.log(person1);
```

## es6-powered class with methods

Do the same thing in a much prettier way, which is known as syntactic sugar.

> JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. 

> **What is Syntactic sugar?**
> 
> In computer science, syntactic sugar is syntax within a programming language that is designed to make things easier to read or to express. 

```
//Class
class Person {
  constructor(firstName,lastName,dob) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = new Date(dob);
  }
  
  getBirthYear() {
    return this.dob.getFullYear;
  }
  
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

  //Intantiate object
  const person1 = new Person('John', 'Doe', '4-3-1980');
  
console.log(person1.getBirthYear());
console.log(person1.getFullName());
console.log(person1);
```