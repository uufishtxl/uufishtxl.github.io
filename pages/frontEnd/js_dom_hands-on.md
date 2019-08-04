---
# layout: note_tutorial
title: Get hands-on with DOM manipulation
catalog: true
tags: 
  - javascript
  - dom
permalink: js_dom_hands-on.html
folder: frontEnd
summary: 
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Remove an element

-   Method: `remove()`

```
const ul = document.querySelector('.items');

ul.remove();
```

## Remove the last element child

-   Property: `lastElementChild`
-   Method: `remove()`

```
const ul = document.querySelector('.items');

ul.lastElementChild.remove();
```

## Change the text content of the 1st element child

-   Property: `firstElementChild`
-   Property: `textContent`

```
const ul = document.querySelector('.items');

ul.firstElementChild.textContent = 'Hello';
```

## Change the text of the 2nd element child

-   Property & index: `children[1]`
-   Property: `InnerText`
-   Property: `innerHTML`

```
const ul = document.querySelector('.items');

ul.children[1].innerText = 'Brad';
ul.lastElementChild.innerHTML = '<h4>Hello</h4>';
```

## Change the styling of an element

```
const btn = document.querySelector('.btn');

btn.style.background = 'red';
```

## Print out log upon an event

-   Method: `addEventListener`
-   Method: `preventDefault()`

1.  Locate the target using the `querySelector()` method.
2.  Add the `addEventListener` function.
3.  Set up the **function** to be called when **the desired event**, in this case, `click` is delivered to the target.
4.  Prevent the default behavior as a result of the event using `preventDefault()`.

```
const btn = document.querySelector('.btn');

btn.addEventListener('click', (e) => {
  e.preventDefault();
  console.log('click');
});
```

## Add a class to an element upon an event

-   Method: `addEventListener`
-   Property: `style` / `background`
-   Method: `classList.add()`
-   Property: `.lastElementChild.innerHTML`

```
const myForm = document.querySelector('#my-form');
const btn = document.querySelector('.btn');
const ul = document.querySelector('.items');

btn.addEventListener('click', (e) => {
  e.preventDefault();
  myForm.style.background = '#ccc';
  document.querySelector('body').classList.add('bg-dark');
  ul.lastElementChild.innerHTML = '<h1>Hello</h1>'
  
})
```

## A complex, and thourough example

-   Event: `submit` - fires when a `<form>` is submitted
-   Method: `querySelector()`;
-   Method: `addEventListener()`;
-   Method: `preventDefault()`;
-   Method: `classList.add()`;
-   Method: `setTimeout()`;
    setTimeout(*function*, *milliseconds*， *param1*, ...): Execute a function after a given period
-   Method: `createElement()`;
-   Method: `appendChile()`;
-   Method: `createTextNode()`;

```
const myForm = document.querySelector('#my-form');
const nameInput = document.querySelector('#name');
const emailInput = document.querySelector('#email');
const msg = document.querySelector('.msg');
const userList = document.querySelector('#users');

myForm.addEventListener('submit', onSubmit);

function onSubmit(e) {
  e.preventDefault();
  if (nameInput.value === '' || emailInput.value === ''){
    msg.classList.add('error');
    msg.innerHTML = 'Please enter all fields!';
    setTimeout(() => msg.remove(), 3000);
  }else {
    const li = document.createElement('li');
    li.appendChild(document.createTextNode(`${nameInput.value}: ${emailInput.value}`));

    userList.appendChild(li);

    //clear fields
    nameInput.value = '';
    emailInput.value = '';
  }
}

```





