---
layout: post
title: Define Response Schema
subtitle: Step by step response schema definitions
date: 2019-07-10
author: edith
header-img: "img/post_bg_coding.jpg"
catelog: true
tags: 
  - Api_docs
  - response
  - schema
---

# Response example

```
{
  "data": [
    {
      "created_time": "2016-08-23T13:12:10+0000",
      "id": "1308573619175349"        // Photo ID
    },
    {
      "created_time": "2016-08-05T22:34:19+0000",
      "id": "1294456907253687"        // Photo ID
    },
    {
      "created_time": "2016-04-29T16:17:02+0000",
      "id": "1228552183844160"        // Photo ID
    }
  ]
}
```

## Step 1: Define the primary layer of your response schema

In the first place, this is a hash mapping. It has a single property, *data*.

```
responses: 
  "200":
    description: Success
    content:
      application/json:
        schema: 
          type: object
          properties:
            data:
              $ref: '#/components/schemas/data'

```

## Step 2: Move on to the second layer

Now, let's proceed to the definition of its value part, in this case, an array. Unlike a dictionary, it consists of several *items*. 
```
components:
  schemas:
    data:
      type: array
      items:
        $ref: '#/components/schemas/Data'
```

## Step 3: Continue to expand on array definition

The array has several objects, each of which consists of a property and a scalar. Congratulations! You are almost finished, given that there's no need to expand on scalars.

```
components:
  schemas:
    Data:
      type: object
      properties: 
        created_time: 
          type: string
          example: "2017-12-08T01:08:57+0000" 
        message:
          type: string
          example: Love this puzzle. One of my favorite puzzles
        id: 
          type: integer
          format: int64
          example: 201906094894  
```

## Oops! What if I prefer having several items in my reponse example on Swagger Editor?

Take a look at the above procedures? Ring any bells?  Properties each have an example. Wipe them out and append a whole-some example to your response:

```
      responses:
        "200":
          description: Successful responses
          content:
            application/json:
              schema: 
                type: object
                properties:
                  data:
                    $ref: '#/components/schemas/data_photo'
                example: 
                  {
                    "data": [
                      {
                        "height": 720,
                        "width": 720,
                        "id": "1308573619175349" 
                      },
                      {
                        "height": 720,
                        "width": 720,
                        "id": "1294456907253687"
                      },
                      {
                        "height": 180,
                        "width": 180,
                        "id": "1228552183844160" 
                      }
                    ]
                  }
```

## Summary

### Array and object

An object has at least one property, while array one item.

### Terminology

- Hash / Mapping / Object / Dictionary
- Array
- Scalar
- Property
- Item
- Key-value pair