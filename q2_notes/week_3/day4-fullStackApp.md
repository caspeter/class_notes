# Full Stack App

- [ ] create github repo

- [ ] clone to local

- [ ] create server.JavaScript file

- [ ] `echo "node_modules" > .gitignore`

- [ ] `cat .gitignore`

- [ ] `npm init --yes`

- [ ] `yarn init --yes`

- [ ] `yarn add express --save`

- [ ] in server.js

      - [ ] `var express = require('express')`
      - [ ] `var app = express();`
      - [ ] `app.listen('3000', function(){console.log('listening on port 3000')})`

- [ ] check to make sure it can listen with `nodemon`

- [ ] git commit/push

- [ ] create a routes folder

- [ ] create index.js file

- [ ] in index.js

      - [ ] require express

      - [ ] at the bottom add `module.exports = route;`

      - [ ] create get route

            - [ ] ```javascript
                  route.get('/',(req, res, next) => {
                    //code goes here
                  })
                  ```


- [ ] server.js

      - [ ] `var index = require('./routes/index')`
      - [ ] `app.use('/', index)` after it has been required

- [ ] git commit/push

- [ ] duplicate index.js, rename it to users.js

- [ ] in the server.js file require the new users file and then `app.use` that users.js file

- [ ] git commit/push

- [ ] in users add a `route.post('/')` to the user file

- [ ] install body-parser, `yarn add body-parser --save`

- [ ] server.js require body-parser

      - [ ] we decided to use the url encoded and the json version, found those in the docs for body-parser

- [ ] test out in postman that we can receieve back what we send in the req.body

- [ ] git commit/push

- [ ] create a public folder

      - [ ] add a new file called index.html
      - [ ] add basic stuff to index.html

- [ ] in sever.js add `app.use(express.static('public'))` to link the server to the index.html page

- [ ] git commit

- [ ] in public create login.html

      - [ ] add a form 

      - [ ] ```html
            <form action="\users" method="POST">
            	<label for="username">User Name<input type="text" name="username" id="username"></label>
            	<label for="password">Password<input type="password" name="password" id="password"></label>
              <button>
               submit button goes here 
              </button>
            </form>
            ```


- [ ] add to the server.js a app.use

- [ ] git commit

- [ ] hash the password

      - [ ] `yarn add bcrypt --save`

      - [ ] in the users.js file require bcrypt

      - [ ] look at the docs for bcrypt

      - [ ] add var hash =

      - [ ] then send back the `username: req.body.username, hash:hash`

            now we need to store this info somewhere

- [ ] install knex `yarn add knex --save`

- [ ] install pg

- [ ] `knex init`

- [ ] createdb dbname

- [ ] change knexfile.js to have a postgres connection

- [ ] `knex migrate:make migratefilename`

- [ ] inside that migrate file:

      - [ ] ```javascript
            return knex.schema.createTable('users', function(table){
              table.increments();
              //other table columns
            })
            ```

      - [ ] and drop the table in the other section `return knex.schema.dropTable`

- [ ] migrate the database `knex migrate:latest`

- [ ] git commit

- [ ] now we need to use knex in our user.js file

      - [ ] require knex `require('knex')(db)`
      - [ ] get the connection information `var require = ('../knexfile.js')['development']`

- [ ] in the users.js, route.post

      - [ ] add

      ```javascript
      var hash = bcrypt
      knex('users')
      .where({username: req.body.username})
      .then(function(results){
        if (results.length === 0){
          //TODO -- add the user
          knex('users')
          .insert({
            username: req.body.username,
            password_hash: hash
          })
          .then(function(result){
            res.sendStatus(201)
          })
          .catch((err) => {
            next(err)
          })
        } else{
          res.status(400).send('User Already Exists')
        }
      })
      ```


- [ ] commit
- [ ] when you get from users, you should be able to get all the users

```
route.get('/' (req,res,next) => {
  knex('users')
})
```

- [ ] create a `route.delete` for users
- [ ] create migration for adminPermission
- [ ] fill in the new migration with alterTable, alter the table 'users' so that there is a isAdmin column
- [ ] seed with an admin, hash the password in that seed file
- [ ] create a new file in public - login.html
      - [ ] will be similar to the registration page
- [ ] ​