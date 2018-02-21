# Lesson 4: Databases (MongoDB)

This lesson will introduce you to some of the core concepts of databases such as the `CRUD` (CREATE, READ, UPDATE, DELETE) operations, NoSQL tables, and Object Modeling. We will be creating a dog adoption website! This is relatively challenging project with many parts, so definitely don't feel afraid to ask for help.


## Part 1: Setup

**Setting up the project**

Navigate into the `lesson-4-skeleton` folder. Create a Node.js project by typing the following:
```javascript
npm init
```
You should now see a `package.json` file inside your project directory.

Make sure to install Express as a dependency.
```javascript
npm install --save express
```

**Creating the Express.js project**
Make sure you are in the same directory with `package.json`. You should have the express CLI globally installed from the previous projects. If you don't, type `npm install --g express-generator`.
```javascript
express --view=ejs
```
This creates an Express application in your current directory and sets `ejs` to the default view engine. In addition, it adds a bunch of dependencies to your `package.json`, so don't forget to type `npm install`! 

**Copying over the views from the lesson-4-completed**

Navigate into the lesson-4-completed folder and copy over the views directory into the lesson-4-skeleton, replacing over the one that express generated.

## Recommended Resources

- Mongoose CRUD reference: https://coursework.vschool.io/mongoose-crud/
- Mongoose Docs: http://mongoosejs.com/index.html
- Promise.all: https://developer.mozilla.org/enUS/docs/Web/JavaScript/Reference/Global_Objects/Promise/all
-  ES6 Arrow Functions: https://codeburst.io/javascript-arrow-functions-for-beginners-926947fc0cdc


