---
# layout: note_tutorial
title: 2.1 Sever-side with Node.js
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_node_js.html
folder: frontEnd
summary: 
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/wxbQP1LMZsw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Use Node.js to create a server locally on your computer for the sake of data persistence. Rather than merely fetching data on a client-based programming tool, you can even save data with Node.js.

## Node.js

> Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. 

With Node, you can write JavaScript without the browser. The code runs on your computer instead of on a browser.

## Express, a node package

### What is node package?

One of the ways that is very typical when working with Node is to find a package -- a node package -- that has some of the functionality you're looking for. It's like a library or add-on. Install the package and make use of its functionality.

### What is npm?

How do we access the node package known as Express? NPM stands for Node Package Manager. It's a thing to manage all of your node packages. It comes along with Node.js. That is to say, you do not have to install it. 

### package.json

To use NPM with this project, we need `package.json`. `package.json` is basically the configuration file for your project. This is where all the meta information about our project, such as what node packages we're using, what our project is called.

To create a `package.json` file, of course you may just make a file called `package.json` and type stuff into it. However, there's a nice command-line utilify from NPM itself to generate the file for you, making sure you don't make wrong of it. Run this: `npm init`, and follow the screen instructions to configure the numerous things.

When you have finished and save the file, you are expected to find everything in there in a file called `package.json`. The reason why we need this `package.json` is in this file is where we need to make reference to Express. Now, you are ready to install Express. 

### What is Express?

A pretty minimal and simple framework for making web servers.

To install Expess, run this: `npm install express`.

When this finishes, two things are gonna happen. Number one is we're going to see Express pop-up in `package.json` as one of the dependencies. The other thing is that we have a new folder called node_modules. Just leave it as-is. They are the numerous dependencies Express requires and you don't actually need to manage it.

## Step 1: Access the express package

> `require()`: The require() method is used to load and cache JavaScript modules. So, if you want to load a local, relative JavaScript module into a Node.js application, you can simply use the require() method.

```JavaScript
const express = require('express');
```

## Step 2: Create a web application

> `express()`: The whole library basically comes in as a big function called `express()`.

```JavaScript
const app = express();
```

## Step 3: Listen to outside requests

Configure a port to listen to outside requests.

```JavaScript
app.listen(3000, () => console.log('Listening at 3000'));
```

## Step 4: Serve a web page

The simpliest thing we want the server to do: 

-   Serve web pages, like `index.html`.

Make a public folder to host publicly accessible web pages and serve the page up in your server code blocks. `index.html` is a default, so you don't have to explicitly specify it.

```JavaScript
app.use(express.static('public'));
```


-   Routing
-   JSON Parsing
-   POST with fetch()
