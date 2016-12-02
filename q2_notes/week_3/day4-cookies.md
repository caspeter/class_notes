# Authorization

**Registraion piece** - supply username/password -> hash password -> store credentials in database -> store the credentails for the client

**Login piece** - supply username/password -> gets credentails from database -> compare hashes -> store the credentails for the client (authorization)

Storing Credentials on the client

#### Cookies

- small - max 4kb (for all cookies)

- set by the server

  in the response header

  set-cookie

- the browser sends all cookies it has stored in the request, for that server

  cookie header

  key/value pairs


- Cookie Expirations
  - Session cookies - deleted after the browser has quit
  - Persistent Cookie - deleted after a specified period of time
- cookie-parser
  - read a cookie - `req.cookies;`
  - set cookie `res.cookie(name, val[,options]);`
  - clear a cookie `res.clearCookie(name[,options]);`
- Code Along:

1. `npm install --save cookie-parser`

2. require cookie-parser

3. `app.use(cookieParser());`

4. ```javascript
   app.get('/', function(){
   	res.cookie('name', 'Mat')
   	res.send();
   })
   //res.cookie's default is a session cookie
   ```

5. ```
   // to see the cookies
   app.get('/cookie', function(){
     res.json(req.cookies)
   })
   ```

- Cookie Security
  - always use HTTPS
  - Indivate to the browser that the cookie should be secure
    - Secure:true option to setCookie
- Cross Site Scripting
  - hacker added malicious javascript - that can read document.cookie and can send it back to the hacker
  - Set HTTPOnly Flag
    - tells the browser to now allow JavaScript to access the cookie
- Brute Force/Guessing
  - a hacker sees the format of your cookie
    - example userId: 3
  - Starts making requests and guessing
  - What we can do?:
    - signed cookies
      - value + cryptographic signautre
    - add encryption key when adding middleware

#### Sessions

sessions do not equal cookies

sessions store a unique id that map to some data for a session

sessions can be stored in cookies, database, MemCache, etc.

cookie session is an abstraction

it stores session data in cookies - but does it in the same way other session providers do. Using `req.session`

This allows you to swap out cookie-session for any other session handler without changing the underlying code

cookie-seesion has sensible defaults:

​	HTTPOnly

​	secure over HTTPS

​	signed and encrypted cookie values

​	a simpler API



#### Middleware

application-level

route-level

substack-level

​	you can stack functions in a route



------



Look up yarn, similar to npm - `yarn why (folder in node_modules)`

npm docs (npm package), can also do `npm repo` or `npm home`