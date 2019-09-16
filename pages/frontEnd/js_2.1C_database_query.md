---
# layout: note_tutorial
title: Database query
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_database_query.html
folder: frontEnd
summary: 
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/q-lUgFxwjEM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Make a `GET` request to a route on the server and have the route return all the data from the database.

## Step 1: Eatablish a route

Establish a route on the server and the client sides to make handshake possible.

### 1-A: Client side

```JavaScript
// run function
getData();
// make a function
async function getData() {
  // For a GET request, you don't have to explicitly specify the method, given that GET is the default. You still can still use /api because its GET route are not occupied
  const response = await fetch('api');
  const data = await response.json();
  console.log(data);
}
```

Uptill now, it doesn't really work. You have to complete the route on the server side. 

### 1-B: Server side

```JavaScript
app.get('api', (request, response) => {
  response.json({test: 123});
});
```

Restart the node.js service and access the page. You may see the printout on your dev console.

## Step 2: Query the database and find everything

```JavaScript
app.get('/api', (request, response) => {
  database.find({}, (err, data) => { // leave the curly braces empty to find everything in the database
    // error handling
    if (err) { 
      response.end();
      return;
    }
    response.json(data);
  });
});
```

## Step 3: Receive and parse data on client

```JavaScript
for (item of data) {
  const root = document.createElement('div'); // root div
  const geo = document.createElement('div'); // accommodate geolocation information
  const date = document.createElement('div'); // accommodate date information

  // Add text to div elements:
  geo.textContent = `Latitude: ${item.lat}°, Longitude: ${item.lon}°`
  // Covert timestamp to readable date strings: 
  const dateString = new Date(item.timestamp).toLocalString();
  date.textContent = `Date: ${dateString}`;

  // specify the hierarchy position of the three div elements
  root.append(geo, date);
  document.body.append(root);
};
```