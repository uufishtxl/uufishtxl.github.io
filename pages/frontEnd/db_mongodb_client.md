---
# layout: note_tutorial
title: MongoDB Basics
catalog: true
tags: 
  - database
permalink: mongodb_basics.html
folder: frontEnd
summary: 
# sidebar: api_sidebar
# topnav: topnav
---

This is based on Traversy Media's video tutorial on **MongoDB Crash Course 2019**.

[MongoDB cheet sheet](https://gist.github.com/bradtraversy/f407d642bdc3b31681bc7e56d95485b6)

## Resource

<p><iframe width="560" height="315" src="https://www.youtube.com/embed/-56x56UppqQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>

## NoSqL

NoSql stands for "not only SQL", is an alternative to traditional relational databases (*关系数据库*) in which data is placed in tables and data schema is carefully designed before the database is built.


## Mongo shell and Compass

-   Compass, a GUI application
-   Mongo shell: Go to `C:\Program Files\MongoDB\Server\4.2\bin\mongo.exe` to run an executable. The command prompt appears afterwards, running Mongo.

## MongoDB Shell Commands

### Show all databases

```
show dbs
```

### Access/Create a database

```
use dbname
```

If the database does not exist, it will create one. However, `show dbs` does not display a blank database.

### Show collections

```
show collections
```

### Drop a database

Use the database and type the command line below.

```
db.dropDatabase()
```

### Show the current database

```
db
```

### Create a collection

```
db.createCollection('posts')
```

### Show collections

```
show collections
```

### Insert data

Data, documents, rows and records can be used interchangeably in a MongoDB context.

#### Insert one row

```
db.collectionName.insert()
```

For example:

```
db.posts.insert({
    title: 'Post One',
    body: 'Body of post one',
    category: 'News',
    like: 4,
    tags: ['news', 'events'],
    user: {
        name: 'John Doe',
        status: 'author'
    },
    date: Date()
})
```

#### Insert many rows

```
db.collectionName.insertMany()
```

For example,

```
db.posts.insertMany([
    {
        title: 'Post Two',
        body: 'Body of post two',
        category: 'Technology',
        date: Date()
    },
    {
        title: 'Post Three',
        body: 'Body of post three',
        category: 'News',
        date: Date()
    },
    {
        title: 'Post Four',
        body: 'Body of post four',
        category: 'Entertainment',
        date: Date()
    }
])
```

Note that in this array, we don't have information about the tags or the user. This is okay since unlike relational database,  MongoDB doesn't have that strict data model that we have to follow.

### Query the data

```
db.collectionName.find()
```

#### Prettify the data

```
db.collectionName.find().pretty()
```

#### Narrow-down

Add something like a where clause.

```
db.collectionName.find({ category: 'News' }).pretty()
```

#### Sort the results

1 for ascending, negative 1 for descending.

```
db.collectionName.find().sort({ title: 1 }).pretty()
```

#### Count documents

```
db.collectionName.find({ category: 'News' }).count()
```

#### Limit the results shown

```
db.posts.find().limit(2)
```

Sort and limit:

```
db.posts.find().sort({ title: -1 }).limit(2)
```

#### For each loop

```
db.posts.find().forEach(function(doc) {print('Blog post: ' + doc.title) })
```

#### Find one particular result

```
db.posts.findOne({ category: 'News'})
```

It should just return the first one.


#### Update data

```
db.collectionName.update()
```

You may pass in three parameters. The first one for the query condition, the second the updates, the last `upsert`, purposed for telling the system that when the result is not found, just insert it.

This method just replaces everything. That's why typing the following command erases the old category information.

```
db.posts.update({ title: 'Post Two' }, 
    {
        title: 'Post Two',
        body: 'New post 2 body',
        date: Date()
    },
    {
        upsert: true
    }
)
```

If you want to keep the missing attributes in your update intact, opt to enclose your update within a `$set` operator.

```
db.posts.update({ title: 'Post Two' }, 
    {
        $set: {
            body: 'Body of post 2',
            category: 'Technology'
        }
    }
)
```

#### Increment operator

Use the `$inc` operator.

```
db.posts.update({ title: 'Post One'},
    { $inc: {likes: 2}}
)
```

#### Rename a field

Use the `$rename` operator.

```
db.posts.update({ title: 'Post One'},
    {$rename: {likes: 'views'}}
)
```

#### Remove a record

```
db.posts.remove({ title: 'Post Four'})
```

#### Sub-documenting

```
db.posts.update({ title: 'Post One' },
    {
       $set: {
           comments: [
               {
                   user: 'Mary Williams',
                   body: 'Comment One',
                   date: Date()
               },
               {
                user: 'Harry White',
                body: 'Comment Two',
                date: Date()
            }
           ]
       } 
    }
)
```

#### Find by element in array ($elemMatch)

```
db.posts.find({
    comments: {
        $elemMatch: {
            user: 'Mary Williams'
        }
    }
})
```

#### Add indexes

```
db.posts.createIndex({ title: 'text'})
```

#### Text search

```
db.posts.find({
    $text: {
        $search: "\"Post O\""
    }
})
```

### Greater than & less than

```
db.posts.find({
    views: {
        $gt: 3
    }
})
```

`$gte` = greater than or equal to

`$lt` = less than

`$lte` = less than or equal to

## Terminilogy

| collection | similar to a table, holds documents of data |
| document | similar to an object |