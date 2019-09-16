---
# layout: note_tutorial
title: 1.1 fetch()
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_fetch_image.html
folder: frontEnd
summary: Fetch an image and create an img element
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/tc8DU14qX6I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Fetch an image, grab its blob information and make an image element.

### Step 1: Fetch the target resource

Call fetch(*path*).

```JavaScript
fetch('rainbow.jpg')
```

### Step 2: Deal with the response

This involves the idea of a **Promise**. Accroding to MDN:  

> The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.  
> 
> The `fetch()` function is a function that happens asynchronously. meaning we call `fetch()`, but some time passes because it takes some time to retrieve the data.
> 
> The `then()` method returns a Promise. It takes up to two arguments: callback functions for the success and failure cases of the Promise.

### Step 3: Complete data stream

However, the response is a stream of data. So we have to read it and pick up what is essential to us and store it in a desired format.

> The blob() method of the Body mixin takes a Response stream and reads it to completion. It returns a promise that resolves with a Blob.

```JavaScript
fetch('rainbow.jpg')
  .then(response => {
    return response.blob();
  })
```

### Step 4: Make an <img> element with that data.

```JavaScript
fecth ('rainbow.jpg')
  .then(response => {
    return response.blob();
  })
  .then(blob => {
    document.getElementById('rainbow').src = URL.createObjectURL(blob);
  })
```

> The URL.createObjectURL(object) static method creates a DOMString containing a URL representing the object given in the parameter. 

### Step 5: Complete the error part

> The catch() method returns a Promise and deals with rejected cases only.

```JavaScript
fetch('rainbow.jpg')
  .then(response => {
    return response.blob();
  })
  .then(blob => {
    document.getElementById('rainbow').src = URL.createObjectURL(blob);
  })
  .catch(error => {
    console.log('error');
    console.error(error);
  });
```

### `async` and `await`: A more readable approach

> The async function declaration defines an asynchronous function, which returns an AsyncFunction object. An asynchronous function is a function which operates asynchronously via the event loop, using an implicit Promise to return its result.
> 
> ```JavaScript
> async function name([param[, param[, ... param]]]) {
>    statements
> }
> ```

> An async function can contain an await expression that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and evaluates as the resolved value.

```JavaScript
async function catchRainbow() {
  const response = await fetch('rainbow.jpg');
  const blob = await response.blob();
  document.getElementById('rainbow').src = URL.createObjectURL(blob);
}
```

Add success message and error information: 

```JavaScript
catchRainbow()
  .then(response => {
      console.log('yay')
  })
  .catch(error => {
      console.log('error!');
      console.error(error);
  });
```

        
