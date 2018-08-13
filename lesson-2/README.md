# Lesson 2: HTTP and Routes

To get a good grasp of the basic concepts of HTTP and routing, we will be creating a simplified version of a Reddit-like forum where users can get view pictures of and discuss cute puppies.

![enter image description here](https://scontent-lax3-1.xx.fbcdn.net/v/t31.0-8/20507398_493223817679381_4732876059136539753_o.jpg?oh=28f6f745e6df63cd34d401fd4dc6f098&oe=5AF9A831)
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

----------


## Part 2: Understanding the project structure

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
