# Heroku

- Explain the purpose of **dotenv**

  `require('dotenv').config()` (you have to install the dotenv package, then require it)

  a place to have enviornment info, and is added to your .gitignore

  storing  environment variables in .env `DATABASE_URL=`

  accessing environment variables `process.env.DATABASE_URL`

- Explain **Heroku** CLI syntax to use to get an app with a database up and running

  what is heroku? - deployment platform

  you must have a git repo on the folder you want to put to heroku

  connect git and heroku together - in terminal `heroku create website-name`

  send files to heroku - `git push keroku master`

  Add your database

  ```terminal
  heroku addons:create heroku-postgresql //this is setting up a database on heroku
  heroku run knex migrate:latest
  heroku run knex seed:run
  ```

  open your app - `heroku open`

  debuggin heroku - `heroku logs --tail` or `heroku logs -t` to keep the logs running

  view the shell - `heroku run bash`

- Explain what the cause of some errors could be

  - Error:ENOENT: no such file or directory, open '.env'

    see if env was installed

  - Knex:ErrorPool2 - Error:connect

    didn't install knex, or a database issue

  - Unhandled rejection Error: Pool is destroyed

    this is related to your database

  - unhandled rejection error: select * from "books" - relation "books" does not exist

    didn't migrate

  - Starting process with command 'npm start', nodemon: not found

    this error is on heroku, where nodemon is not found because it was installed globally. look in package.json to see if it is being called. It needs to be a **node server.js in script start**

    OR (do this one ^)

    use proc package