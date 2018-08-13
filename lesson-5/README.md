# Lesson 5: Authentication with Sessions

This lesson will add on to some of the concepts taught in Lesson 4 by adding an authentication layer to API. We will be going over Logging in with Sessions via [passport.js](http://www.passportjs.org/)

<img src="https://i.imgur.com/BzuXuHz.png">

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

## Summary

This is a modified version of the Landing Page on the previous app. First, create a user giving any set of credentials, then log them in by filling out those exact credentials on the Login panel. Upon login, you should be redirected to the Home Page again.

To see if things are working, (if you're on Chrome) open up the Chrome Developer Tools (Shift + Cmd + C) and:

1. Click on the tab that says **Application**
1. Click on Cookies > localhost:3000
1. You should see a cookie that says `connect.sid` which is how `express-session` is storing its cookies.

<img src="https://i.imgur.com/Eg5mVkM.png">

Now you should be able to reload on `localhost:3000/home` without getting authorization errors.

Click on **Logout** and now go to [localhost:3000/home](localhost:3000/home) and suddenly you should see an error saying **Unauthorized Access 401**.

----------

## A Lil' Cryptography Aside

Now, when we store passwords on our database, we don't want to store the plaintext password because that's bad! If a hacker manages to get in our database, they have access to all of our user's passwords.

Instead, our protocol of authentication will be to hash the user's password using a hash function known to be cryptographically secure. When we want to check if the user inputted the correct password, we will hash the input and compare it with the hash in our database.

However, we have another problem. A lot of known password hashes are saved throughout the internet in something known as a **Rainbow Table**. This makes our password hashes as susceptible to hacking as a plaintext password.

Hence, our solution is to hash our password with an additional string called a **salt**. The salt is unknown to the hacker which defends our database from a Rainbow Table attack.

Don't worry though, all this can be done for us with an npm module. Yay!

### Motivation

Passport is an authentication middleware which helps you authenticate requests. In addition, Passport offers multiple methods authentication known as "Strategies". Strategies include Facebook, Google, or even Github OAuth.

Passport allows a very general way our authentication strategies (in the case we need to have multiple login buttons), which makes it easier to integrate a lot of different types of logins.

In this case we will be working with a Local Strategy with authentication involving users in our own database.‎

Our plan of attack is as follows:

1. Find the user associated with the username.
2. Check if the user exists, if the user doesn't exist, return an error via the `done` callback.
3. If the user does exist, check if the password matches the password hash in our database. (We can use `bcrypt` for this)

----------


### Now what is going on? (For the curious)

So you've written all these bits and pieces, but what exactly is going on behind the scenes? Let's go step-by-step on the login process:

1. You pass in your credentials to the login panel and it sends a **POST** request to the server.
2. The server redirects you to the code on `router.post('/login', ...)` which first runs `passport.authenticate('local')`
3. Seeing the key `'local'`, Passport runs the LocalStrategy on the username and password you passed in from the request (Using `request.body`).
4. Once it validates the existence of the user, and a matching password hash, it will call the `done` callback with the user, calling the `serializeUser()` function.
5. `serializeUser()` will return the user's id which will be passed into a Mongo document under the collection `sessions` and stored in the MongoStore.
    1. In addition, this Mongo document's id will be passed to the frontend as a cookie called `connect.sid`
6. Finally, it will run the callback we wrote, sending a **200 OK** request.

Congratulations on creating a working login & authentication system!

----------

**Extra Credit (Implemented)**

> Using the idea of Express' callback chain, and this authentication checker, can you combine the topics to create a reusable middleware to determine if someone's logged in? Also note, that callbacks in Express can actually take in 3 parameters, `res`, `req`, and `next`. `next` is specifically a way to call the next callback in the callback chain.

----------

## Glossary and Useful Links

* https://scotch.io/tutorials/easy-node-authentication-setup-and-local
* http://toon.io/understanding-passportjs-authentication-flow/
* http://cryto.net/~joepie91/blog/2016/06/13/stop-using-jwt-for-sessions/

* http://www.editthiscookie.com/
