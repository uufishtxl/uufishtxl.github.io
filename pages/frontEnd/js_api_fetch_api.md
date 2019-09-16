---
# layout: note_tutorial
title: 1.4 Grab JSON data from REST API
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_fetch_api.html
folder: frontEnd
summary: Grab JSON data from REST API and plot it on a map
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/jKQUHGpOHqg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Fetch data from a REST API and plot it on a map.


### Steps

1.  Fetch data from a REST API.  
    ```html
    <body>
        <p>
            Longitude: <span id="lon"></span><br>
            Latitude: <span id="lat"></span>
        </p>
    </body>
    ```
    
    ```JavaScript
    const apiUrl = 'https://api.wheretheiss.at/v1/satellites/25544' // resource endpoint

    async function getISS() {
        const response = await fetch(apiUrl);
        const data = await response.json();
        const { longitude, latitude } = data; // deconstruction
        document.getElementById('lon').textContent(longitude);
        document.getElementById('lat').textContent(latitude);
    }

    getISS();
    ```  
3. Perparing the page for the map with [`leaflet.js`](https://leafletjs.com/).
    1.  Include the Leaflet CSS file in the head section of the document.
    ```HTML
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
    integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
    crossorigin=""/>  
    ```  
    2.  Include Leaflet JavaScript file after Leaflet's CSS:  
    ```HTML
     <!-- Make sure you put this AFTER Leaflet's CSS -->
    <script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
    integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
    crossorigin=""></script>
    ```  
    3.  Put a `div` element with a certain `id` where you want your map to be:  
    ```HTML
     <div id="issMap"></div>
    ```  
    4.  Make sure the map container has a defined height:  
    ```CSS
    #issMap { height: 180px; }
    ```  
4.  Set up the map.
    1.  Initialize the map and set its view to **our chosen geographical coordinates** and **a zoom level**.
    ```JavaScript
    const mymap = L.map('issMap').setView([0, 0], 1); // [0, 0] Set center, 1 zoom times
    ```
    2.  Add a tile layer to add to our map, in this case it's Open Street Map. This usually involves setting the URL template for the tile images and the attribution text.  
    ```JavaScript  
    const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png';
    const attribution = '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    const tiles = L.tileLayer(tileUrl, { attribution });
    ```  
5.  Add a marker with a custom icon.  
    ```JavaScript  
    const issIcon = L.icon({
    iconUrl: 'iss200.png',
    iconSize:     [50, 32], // size of the icon
    iconAnchor:   [25, 16], // point of the icon which will correspond to marker's location 
    });
    const marker = L.marker([0, 0], {icon: issIcon}).addTo(mymap); // Initialize the position of the marker.
    ```
6.  Let the marker move dynamically.
    ```JavaScript
    const apiUrl = 'https://api.wheretheiss.at/v1/satellites/25544'

    async function getISS() {
        const response = await fetch(apiUrl);
        const data = await response.json();
        const { longitude, latitude } = data;

        marker.setLatLng([latitude, longitude]); // Changes the marker position to the given point.

        document.getElementById('lon').textContent(longitude);
        document.getElementById('lat').textContent(latitude);
    }    
    ```
7.  Place animation on first-time launch of the map.
    ```JavaScript
    const apiUrl = 'https://api.wheretheiss.at/v1/satellites/25544'

    let firstTime = true; // Set the initial boolean value as true;

    async function getISS() {
        const response = await fetch(apiUrl);
        const data = await response.json();
        const { longitude, latitude } = data;

        marker.setLatLng([latitude, longitude]);

        if (firstTime) { // Run setView() only for the first time. After than, change its value to false.
            mymap.setView([latitude, longitude], 4); // Sets the view of the map (geographical center and zoom) with the given animation options. 4 is the zoom level
            firstTime = false;
        }

        document.getElementById('lon').textContent(longitude);
        document.getElementById('lat').textContent(latitude);
    }   
    ```
8.  Get the function to refresh automatically every 2 seconds.
    ```JavaScript
    setInterval(getISS, 2000);
    ```  
    Actually, this is kind of dangerous when it takes more than 2 seconds to complete the data retrieval and rendering. Someone suggests that we should  "loop" with setTimeout() after the fetching is done. Anyway, it's a good point.
9.  Polish the data. Fix numbers to only two decimal points.  
    ```JavaScript
    getElementById('lon').textContent = longitude.toFixed(2);
    ```