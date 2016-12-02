# Knex & Express

##### REST

representational state transfer, a way to structure client-server communication over HTTP

##### What is a RESTful database-driven HTTP server?

- a server that communicates with a client using a RESTful HTTP API
- the sole purpose of the HTTP server is to manage information that's persisted to a database

##### Why is a RESTful database-driven HTTP server useful?

- separation of concerns
- follows the principle of least surprise - logical organization 
- great way to organize data, relationships, processes
- processes are independently scalable and replaceable

Use Express and Knex to build a RESTful server

##### Express

a library built ontop of the http module



##### library vs. framework

framework - highly opinionated library, it extends functionality that is already avaiable. 

library is a toolbox, where there are lots of tools, and you can pick up one and use it individually ex: jQuery

framework is a workshop, where there are a lot of tools, but each tool has its own place and purpose. ex: express

##### Promises

help you sort out your successes and failures

# Schema Dos and Don'ts

Terms: 

- unnormalized

  ​

- normalized

  used to reduce data redundancy and improve data integrity

  the goal is to isolate data, and make lots of small tables to create the database

  rules (First Normal Form):

  ​	no repeating rows

  ​	a primary key, all non key columns are dependent on the primary key

  ​	each field contains only one piece of information (no lists)

- denormalized

  ​