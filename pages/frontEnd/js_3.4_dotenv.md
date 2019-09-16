---
# layout: note_tutorial
title: Address security issues using dotenv
catalog: true
tags: 
  - API
permalink: js_api_dotenv.html
folder: frontEnd
summary: 
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/17UVejOw3zA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Make a `GET` request to a route on the server and have the route return all the data from the database.

Previously, the api key just sits in the code. That's terrifying because once you publish your code to another one or even on Internet, your code will be revealed and risk being abused. 

For this reason, we should import a node package to help to convert a .env file into process.env. With our key in a .env file, we place it in the safest hand.

## Step 1: Install the dotenv package

1.  Launch git back and go to the desired directory.
2.  Type the command: `npm install dotenv`.
3.  Wait several seconds till installation completes.

## Step 2: Import the package into your project

1.  Open the server script.
2.  Import the package into your project with the command `require('dotenv').config()`.

## Step 3: Save your api key in a .env file

1.  Create a file and name it ".env".
2.  Add your api key in this way: `API_KEY` = dc9e484c1abfg4a066e323ae25075d1e`.
3.  Save and exit.

## Step 4: Implicitly quote your api key

You are good to go.

```JavaScript
// Specify where your web system may come with the api key
const api_key = process.env.API_KEY;
const weather_url = `https://api.darksky.net/forecast/${api_key}/${lat},${lon}/?units=si`;
```

## Step 5: Make a .env sample

If you'd like to share your code with other, you're better off making a .env sample to let others know where to place their api keys.

Name your new file like this: ".env_sample".

```
API_KEY =  YOUR_API_KEY_HERE
```

## Step 6: Publish on Github

A .gitignore file specifies the files and folders you'd like to keep them to yourself instead of getting them published on Internet.

```
.env
node_modules/
database.db
```