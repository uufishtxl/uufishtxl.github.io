---
# layout: note_tutorial
title: 1.2 fetch and graph a local CSV
catalog: true
tags: 
  - API
  - fetch()
permalink: js_api_fetch_csv.html
folder: frontEnd
summary: Grab a local csv file ane make a graph
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Daniel Shiffman's video tutorial on **Working with Data and APIs in JavaScript**.

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/RfMkdvN-23o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## Purpose

Fetch a local csv file and make a graph.


### Step 1: Load a local CSV file

1.  Review the source CSV file and clear all the mistakes and empty rows and columns.
2.  Use `fetch()` to fetch its data.
3.  Complete the data stream.

```JavaScript
async function getData() {
  const response = await fetch(`ZonAnn.Ts+dSST.csv`);
  const table = await response.text();
}
```

### Step 2: Manual parsing

1.  Split the data to rows based on line breaks.
2.  Get rid of the header row.
3.  Loop through the rows to get years and temperatures out of the data.
4.  Push the years into the array of X-axis data, the temps the array of Y-axix data.
5.  Remember that in spreadsheets, numbers are expressed as strings. So you have to convert them to numbers using the `parseFloat()` method.

```JavaScript
async function getData() {
  const xs = [];
  const ys = [];
  const response = await fetch('ZonAnn.Ts+dSST.csv');
  const data = await response.text();
  const table = data.split(/\n/).slice(1);
  table.forEach(row => {
    const columns = row.split(',');
    const year = columns[0];
    xs.push(year);
    const temp = columns[1];
    ys.push(parseFloat(temp) + 14);
  })
}
```

### Step 3: chart.js

1.  Summon up the getting started tutorial of `chart.js`.
2.  Copy and paste the example as below on your page.   
    ```JavaScript
    <canvas id="myChart" width="400" height="400"></canvas>
    <script>
    var ctx = document.getElementById('myChart').getContext('2d');
    var myChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            datasets: [{
                label: '# of Votes',
                data: [12, 19, 3, 5, 2, 3],
                backgroundColor: [
                    'rgba(255, 99, 132, 0.2)',
                    'rgba(54, 162, 235, 0.2)',
                    'rgba(255, 206, 86, 0.2)',
                    'rgba(75, 192, 192, 0.2)',
                    'rgba(153, 102, 255, 0.2)',
                    'rgba(255, 159, 64, 0.2)'
                ],
                borderColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                yAxes: [{
                    ticks: {
                        beginAtZero: true
                    }
                }]
            }
        }
    });
    </script>
    ```
2.  Configure data source.  
    In our case, the years should be X-axis labels while the temps Y-axis data. Enable the `getData()` function to return an object literal representing a pair of the desired data. By doing so, we are able to quote such data by using dot notation.  
    ```JavaScript
    async function getData() {
      const xs = [];
      const ys = [];
      const response = await fetch('ZonAnn.Ts+dSST.csv');
      const data = await response.text();
      const table = data.split(/\n/).slice(1);
      table.forEach(row => {
        const columns = row.split(',');
        const year = columns[0];
        xs.push(year);
        const temp = columns[1];
        ys.push(parseFloat(temp) + 14);
      })
      return { xs, ys }
    }
    ```
3.  Organize the `chart.js` related code lines into a function.  
    ```JavaScript
    async function chartIt() { // Organize the `chart.js` related code line into a function
          const data = await getData(); // Get resulting data from the getData() function.
          const ctx = document.getElementById('myChart').getContext('2d');
          const myChart = new Chart(ctx, {
              type: 'line', // Switch the graph to a line chart
              data: {
                  labels: data.xs, // Customize the label sources
                  datasets: [{
                      label: 'Combined Land-Surface Air and Sea-Surface Water Temperature (℃)', // new name
                      data: data.ys, // Customize the data source for the Y-axis
                      fill: false, // Do not fill the line
                      backgroundColor: 'rgba(255, 99, 132, 0.2)', // Adopt single color scheme across different datasets
                      borderColor: 'rgba(255, 99, 132, 1)', // adopt single color scheme across different datasets
                      borderWidth: 1
                  }]
              },
              options: {
                  scales: {
                      yAxes: [{
                          ticks: {
                              // Include a ℃ sign in the ticks
                              callback: function(value, index, values) {
                                  return value + '℃';
                              }
                          }
                      }]
                  }
              }
          });
      }
    ```

3.   Call the `chartIt()` function.