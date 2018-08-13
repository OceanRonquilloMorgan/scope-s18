# Lesson 3: Node Modules and APIs

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

## APIs and Project Setup
More specially talking about APIs now, they can be thought of as a protocol for getting information between a source and someone who wants to use it. For example in a weather API, the developer will make a request for information. 

The four common types of HTTP requests are as follows:
* **GET** - Retrieves data from the database
* **POST** - Creates information to your database
* **PUT** - Updates information to your database
* **DELETE** - Removes data from your database

### Clarifai API
Clarifai is an image and video recognition API that we are going to integrate into our project. We are going to build the backend for an program where you input a URL of an image and the webpage will display with the image and a guess for what the image is.

**Sign-up for Clarifai**  

 To get an API Key, sign-up for a free account.  
https://clarifai.com/developer/account/signup/

**Install Clarifai**
  
```
npm install clarifai --save
```

Add this to the top of `index.js`
```JS
const Clarifai = require('clarifai');
```
Then add this below all the require statements. This will get your API key out of the `clarifai.json` file. We need an API key in order to make any calls to the API.
```JS
// API key
const apiKey = require('../config/clarifai.json').key;

// Initialize the API key (Fill out your API key in config/clarifai.json)
const app = new Clarifai.App({
    apiKey: apiKey
});
```
Then open the `clarifai.json` file within the `config` directory and replace with your API key which can be found at
https://clarifai.com/developer/account/keys 
When we're dealing with API keys or sensitive data, it's usually good to decouple it from your JavaScript code and keep it in a configuration file.

----------

## Recommended Resources

A list of cool free public API's are listed below:

- https://github.com/toddmotto/public-apis
- https://github.com/abhishekbanthia/Public-APIs
- https://www.programmableweb.com/apis/directory

A cool one to think about: https://cloud.google.com/natural-language/

<b>To learn more about Clarifai go to their docs</b>
https://www.clarifai.com/developer/docs/
