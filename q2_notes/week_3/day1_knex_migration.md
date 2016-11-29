# Knex Migration & Seeds

What is the **migration system**?

​	a way to automate the management of database tables with Javascript

Why is migration useful?

​	consistancy across development databases, identical db structure

​	amending mistakes is easy, move migration backward (down), fix the mistake, and then move migration forward to implement changes



### Practice Steps:

`.gitignore`

`knexfile.js` makes knex file

```javascript
'use strict';

module.exports = {
  development: {
    //what client are you using? here we are using postgres
    client: 'pg',
    connection: 'postgres://localhost/trail_conditions'
  }
};
```

`knex migrate:make trails` makes a migrations folder and puts a file in there called timestamp_trails

the file will have something like this:

```javascript

exports.up = function(knex, Promise) {
  
};

exports.down = function(knex, Promise) {
  
};

```

Populate the trails file, then run `knex migrate:latest` in the terminal

don't worry about the knex_migrations and knex_migrations_lock tables for now

To make a seed file: `knex seed:make trails`

To roll-back the migration: `knex migrate:rollback`

Seed files are organized and ran by alphabetical order 



### Bookshelves Help

JSON naming

​	is normally camel cased

​	meaningful names with defined semantics

​	first character must be a letter, underscore or a dollar sign

​	following characters can be a number, letter, underscore or a dollar sign

​	reserved JavaScript keywords should be avoided

What do you do if you used an underscore naming convention for your database fields?

​	created_at => createAt

​	node module called humps, `const{ camelizeKeys, decamelizeKeys} = require('humps')`;

​	this happens in the server, when doing CRUD

```
	browser  						server									database
┌─────────────────┐         ┌───────────────────┐					┌───────────────────┐
│                 │         │                   │					│					│
│                 │──── ───▶│                   │─── decamelize ──▶│				   │
│                 │         │                   │					│					│
│                 │         │                   │					│					│
│                 │         │                   │					│					│
│                 │◀──   ──│                   │◀── camelize ──────│				   │
│                 │         │                   │					│					│
└─────────────────┘         └───────────────────┘					└───────────────────┘
```

Throwing errors

​	node module 'boom' (`next(boom.create(400, 'error message to human'))`)

​	centralize error logging

​	ability to handle errors differently in development vs production

​	not "rolling your own" in your routers

Resetting seed data id's

​	`knex.raw("SELECT setval('books_id_seq', (SELECT MAX(id) FROM books))")`



## Express/Router

- Explain what an express router is

  store routes in a separate file, then link them to one file to run all the routes

- Explain why an express router is useful

  you can organize a project's RESTful routes into separate resource-specifc file modules

  avoid merge conflicts

  ```
  |-routes
  |   |-activities.js
  |   |-drinks.js
  |   |-food.js
  |   |-guests.js
  |   |-prizes.js
  |- server.js
  ```

