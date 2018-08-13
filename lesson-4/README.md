# Lesson 4: Databases (MongoDB)

This lesson will introduce you to some of the core concepts of databases such as the `CRUD` (CREATE, READ, UPDATE, DELETE) operations, NoSQL tables, and Object Modeling. We will be creating a dog adoption website! This is relatively challenging project with many parts, so definitely don't feel afraid to ask for help.

<img src="https://camo.githubusercontent.com/341cd86c4d2c3c0afb76fa13573f6f006d9fe250/68747470733a2f2f692e696d6775722e636f6d2f4d554d63654b7a2e706e67">

<img src="https://camo.githubusercontent.com/bc3aa82671c8d90a933a14fe58e1c8e3bca03946/68747470733a2f2f692e696d6775722e636f6d2f435062563065442e706e67">


## Setup
**node.js**
Make sure to you have the right version of Node.js
```
node -v
// -> should print 8.x
npm -v
// -> should print 5.x
```
### Installing

**Install dependencies**
```
npm install
```

### Running the project
Make sure you are in the same directory with `package.json`.
```
npm start
```

### Check it out
Open a new tab and go to
```
localhost:3000
```

----------

## Introduction to Mongoose
**Benefits of Mongoose**

Although we could technically use MongoDB with its native driver (http://mongodb.github.io/node-mongodb-native/3.0/), it requires a lot of configuration and a lot of code to be written in order to perform basic operations.

Here is an example with the native driver detailing a `CREATE` operation:
```javascript
const { MongoClient } = require('mongodb');

MongoClient.connect(url, (err, client) => {
  const db = client.db(dbName);

  // Insert a single document
  db.collection('dogs').insertOne({
       name: 'Spot',
       breed: 'French Terrier',
       gender: 'female',
       birthday: 'Fri Aug 16 1985 00:00:00 GMT-0400 (EDT)',
    },
    {
        w: 'majority',
        wtimeout: 10000,
        serializeFunctions: true,
    }, (err, r) => {
    assert.equal(null, err);
    assert.equal(1, r.insertedCount);
    client.close();
  });

// disgusting.
```
With Mongoose, it can be as simple as:
```JS
const mongoose = require('mongoose');
const Dog = require('../models/Dog');

mongoose.connect(url);

const dogPromise = new Dog({
    name: 'Spot',
    breed: 'French Terrier',
    age: 5,
    gender: 'female',
});

dogPromise.save()
    .then((dog) => {
        assert.equal(dog.name, 'Spot');
    })
    .catch(err => assert.equal(null, err));
```
**Schemas and Models**

In addition to Mongoose allowing us to write more user-friendly code via Promises, it also allows us to define Schemas for our objects. Schemas make our data more structured and have built-in validation for type-checking and missing fields.

An example Schema is as follows:
```javascript
const mongoose = require('mongoose');
const dogSchema = new mongoose.Schema({
    // We can specify type like this:
    name: String,
    // Or we can specify type like this with an options Object.
    // We typically only do this if we need to specify more options
    // such as a field being required or not.
    breed: {
        type: String,
        required: true,
    },
    age: Number,
    gender: Number,
});
```
In addition to creating a `schema`, we have to create a `model` that corresponds to it. A `model` is a one-to-one mapping between a Mongoose schema and an entry in the database.

Defining a model is as simple as follows:
```javascript
const Dog = mongoose.model('Dog', dogSchema);
module.exports = Dog;
```
The first parameter is the name of the model, which we use in performing `CRUD` operations on the database. The second parameter is the schema object which we have defined above. By calling `mongoose.model(...)`, we are explicitly telling MongoDB to create a `collection` in our database called `dogs` (it takes the first parameter, transforms it to lowercase, and pluralizes it). Whenever we perform a `CRUD` operation with `Dog`, we will only be using our `dogs` collection. We also want to export our model so that we can import it from our route code.

**Validation**

If we try to insert an erroneous document:
```javascript
const badDogPromise = new Dog({
    name: 'Daisy',
    age: 9,
    gender: 'female',
});

badDogPromise.save()
    .then((dog) => {
        // Control flow will never hit here
    })
    .catch(err => console.log(err));
// Error: field 'breed' was marked as required!
```
Mongoose's built-in validation allows us to check whether or not our database operations were successful in our routes, and return appropriate HTTP responses.

Let's see it all in action!

----------

## Recommended Resources

- Mongoose CRUD reference: https://coursework.vschool.io/mongoose-crud/
- Mongoose Docs: http://mongoosejs.com/index.html
- Promise.all: https://developer.mozilla.org/enUS/docs/Web/JavaScript/Reference/Global_Objects/Promise/all
-  ES6 Arrow Functions: https://codeburst.io/javascript-arrow-functions-for-beginners-926947fc0cdc


