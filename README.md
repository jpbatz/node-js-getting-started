# node-js-getting-started

0) Sign up for account on https://dashboard.heroku.com

1) Download Heroku Toolbelt from https://devcenter.heroku.com

2) From your terminal window:

$ heroku login
(same account information from item 0)

Your project:

$ git clone ...                       // creates package.json

$ cd ...

$ heroku create                       // creates heroku remote and generates a random name

$ git push heroku master              // deploy to heroku
                                      // needs your public ssh key from ~/.ssh/id_rsa.pub -> heroku settings
                                      
$ heroku ps:scale web=1               // runs 1 instance
                                      // scaling: 1 = single web dyno
                                      
$ heroku open                         // launch app

$ heroku logs --tail                  // view logs (refresh site to see entry)
^c to stop

$ cat Procfile                        // dyno = single lightweight container that runs the command specified in Procfile
web: node index.js                    // web = attaches to HTTP routing stack and recieves web traffic when deployed
                                      // node = command to execute when app starts
                                      // index.js = app
                                      
$ heroku ps                           // see dynos
                                      // 1 dyno is free, but will sleep after 1 hour, 
                                      //   and cause a momentary delay for the first requestor to wake it up
                                      // 2 dynos will not cause wake up delay, but not free 
                                    
$ foreman start web                   // run app locally
^c to stop                            // see port #
                                      // view page with: web browser or $ curl localhost:[port]
                                      // also sets "config vars"

# Provisioning
==============

add-ons = 3rd Party cloud services ($fee$)

$ heroku addons:add papertrail         // logging service, 1500 lines

$ heroku addons                        // lists add-ons

$ heroku addons:open papertrail        // opens console

# Run REPLs

$ heroku run node
^c ^c to stop

$ heroku run bash
$ exit 
$ exit

# config vars - environment variables
=====================================

ex.
   index.js
      .
      .
      .
      var TIMES = process.env.TIMES || 5;
      
$ heroku config:set TIMES=2

$ heroku confing                      // view config vars


# Provisioning a Database
=========================

$ heroku addons: add heroku-postgresql:hobby-dev

// creates database
// set DATABASE_URL environment variable

$ heroku config                       // to see DATABASE_URL

$ vi package.json                     // add dependency
                                      // "pg": "4.x",
                                      
$ npm install

$ edit index.js

  // add /db route
  // connect with DATABASE_URL

$ heroku pg:psql

  => create table test_table (id integer, name text);       // insert table
  => insert into test_table values (1, 'hello database');  // insert record
  => \q

$ heroku foreman start web              

http://secure-basin-9103.herokuapp.com                     // browse to database



Getting Started With NodeJS on Heroku:
======================================

A barebones Node.js app using [Express 4](http://expressjs.com/).

This application support the [Getting Started with Node on Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs) article - check it out.

## Running Locally

Make sure you have [Node.js](http://nodejs.org/) and the [Heroku Toolbelt](https://toolbelt.heroku.com/) installed.

```sh
$ git clone git@github.com:heroku/node-js-getting-started.git # or clone your own fork
$ cd node-js-getting-started
$ npm install
$ npm start
```

Your app should now be running on [localhost:5000](http://localhost:5000/).

## Deploying to Heroku

```
$ heroku create
$ git push heroku master
$ heroku open
```

## Documentation

For more information about using Node.js on Heroku, see these Dev Center articles:

- [Getting Started with Node.js on Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs)
- [Heroku Node.js Support](https://devcenter.heroku.com/articles/nodejs-support)
- [Node.js on Heroku](https://devcenter.heroku.com/categories/nodejs)
- [Best Practices for Node.js Development](https://devcenter.heroku.com/articles/node-best-practices)
- [Using WebSockets on Heroku with Node.js](https://devcenter.heroku.com/articles/node-websockets)
