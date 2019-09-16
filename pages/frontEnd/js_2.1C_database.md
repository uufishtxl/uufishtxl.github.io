---
# layout: note_tutorial
title: Save to a Database
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_node_database.html
folder: frontEnd
summary: 
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/xVYa20DCUv0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Save data into a database.

## Step 1: Connect to the backend database

```JavaScript
const Datastore = require('nedb');
const database = new Datastore('database.db'); // Make the database and give it a path to the file name
```
At this time, you can't find such a file on your laptop.

## Step 2: Load the databse

```JavaScript
database.loadDatabase();
```

This line means loading the data from the previous time the server ran into memory. If it isn't there, it's going to create the file.


## Step 3: Push data received into your database

```JavaScript
const timestamp = Date.now(); // Get the current time and make it a variable
data.timestamp = timestamp; // Push it into the data object
database.insert(data); // Insert the data object into databse
```