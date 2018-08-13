# Lesson 2: HTTP and Routes

To get a good grasp of the basic concepts of HTTP and routing, we will be creating a simplified version of a Reddit-like forum where users can get view pictures of and discuss cute puppies.

<img alt="lesson-screenshot" src="https://camo.githubusercontent.com/be2f7fc494629837c529c40672500badaa930154/68747470733a2f2f692e696d6775722e636f6d2f464373483636762e706e67">

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


## Understanding the project structure

 - **bin**: Holds the `www` file, whose sole purpose is to actually run your application. Don't worry about this one.
 - **node_modules**: Contains the source code of everything you  `npm install`
 - **public**: All of your static resources to be served are contained here
 - **routes**: All of your routing logic goes here (handling `POST`, `GET`, etc...)
 - **views**: Where your frontend views live.
 - **app.js**: The actual express app itself.


----------

## Recommended Resources

 - Promises: https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261
 - Express Routing: http://expressjs.com/en/guide/routing.html
