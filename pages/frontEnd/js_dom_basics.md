---
# layout: note_tutorial
title: DOM Basics
catalog: true
tags: 
  - javascript
  - dom
permalink: js_dom_basics.html
folder: frontEnd
summary: Obtain base-knowledge of DOM
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## The `window` object

The window object is the parent object of the browser. As the top-level object, you may omit it while implementing dom trees.

For instance, you don't necessarily write `window.alert('This is a message!)`. Just put it like this, `alert('This is a message)`.

## Query selectors

-   getElementById(): Still in use
-   getElementsByClassName(): Depreciated
-   getElementsByTagName(): Depreciated
-   Query selectors:
    -   querySelector(): single selector, means it simply selects the first match
    -   querySelectorAll(): most recommended  
    ```
    console.log(document.querySelectorAll('.item'));
    // equals to console.log(document.getElementsByClassName('item'));
    ```

`querySelector` and `querySelectorAll` works much like JQuery. `querySelector` is a single selector while `querySelectorAll` gives a node list which is quite similar to an array.

### Loop Through

```
// Gives a node list
const items = document.querySelectorAll('.items');

// loop through the node list
items.forEach((item) => console.log('item'));
```