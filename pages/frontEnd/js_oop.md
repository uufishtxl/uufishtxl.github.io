---
# layout: note_tutorial
title: OOP in JavaScript
catalog: true
tags: 
  - javascript
  - oop
permalink: js_oop.html
folder: frontEnd
summary: Class-based programming in JavaScript
# sidebar: frontEnd_sidebar
# topnav: topnav
---

OOP, also known as object-oriented programming

## Resources

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/xoL6WvCARJY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Class

> It is the design or blurprint of any entity, which defines the core properties and functions.

## Object

> An object is an inheritance of a class which has physical existence.
> 
> My name is *edith*, and I am an *object* of class *Female*.
> 
> HumanBeing, Male or Female, we just mean a type/kind.
> 
> You, me, our friends, have physical existence, while class is just a logical definition.

## Inheritance

> In OOP, the meaning of inheritance is very close to its actual meaning in English.
> 
> ![inheritance](/img/oop_inheritance.png)


## Abstraction

> Abstraction means hiding the details from the outside world.
> 
> Get the details hidden from the outside world and take a 'skin' as the abstraction factor to hide the inside mechanism from the outside world.
>
>![abstraction](/img/oop_abstraction.png)


## Encapsulation

> Encapsulation refers to binding properties with functions.

## Polymorphism

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

## A metaphor

-   **class**: HumanBeing

    -   **Properties**: Body Parts
        -   Hands
        -   Legs
        -   Eyes...
    -   **Functions**: Body functions:
        -   Walk()
        -   Talk()
        -   See()