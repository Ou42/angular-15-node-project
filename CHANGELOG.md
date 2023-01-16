## 2023-01-11

### Step 1

- created server.js
- uses express & cors
- created simple route for testing
- tested via: `node server.js`
- browser -> http://localhost:8080/
- browser console shows JSON 'message'

### Step 1b

- created README.md, attributed bezkoder
- listed app/tool vers:

```text
$ nvm --version
0.39.3
$ node --version
v18.13.0
$ npm --version
8.19.3

$ npm ls
...
├── cors@2.8.5
├── express@4.18.2
├── mysql2@2.3.3
└── sequelize@6.28.0
```

### String Interpolation

- requires back-ticks!

## 2023-01-12

### Configure MySQL db & Sequelize

- created ./app/config/db.config.js

### Initialize Sequelize

- created ./app/models/index.js to setup Sequelize
- updated server.js to use Sequelize to sync db

### Define the Sequelize Model

- created ./app/models/tutorial.model.js

### To Do:

- [ ] vscode offers to convert CommonJS module to ES module

### Create the Controller

- created ./app/controller/tutorial.controller.js  
  with the following CRUD functions:
  - create
  - findAll
  - findOne
  - update
  - delete
  - deleteAll
  - findAllPublished

## 2023-01-14

### Things skipped/missed:

- Needed to *install* MySQL  
  <https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/>
- Access mysql via:  
  `mysql -u root -p`  
  <https://dev.mysql.com/doc/mysql-getting-started/en/>
- Needed to `CREATE DATABASE testdb;`

### Finish code for the Controller

- [x] create
- [x] findAll
- [x] findOne
- [x] update
- [x] delete
- [x] deleteAll
- [x] findAllPublished

### Define Routes

- still following "sub-tut" ref'd from 1st:  
  <https://www.bezkoder.com/node-js-express-sequelize-mysql/>
- `tutorial.routes.js`

> When a client sends request for an endpoint using HTTP request (GET, POST, PUT, DELETE), we need to determine how the server will reponse by setting up the routes.
>
> These are our routes:  
> 
> - /api/tutorials: GET, POST, DELETE
> - /api/tutorials/\<id\> GET, PUT, DELETE
> - /api/tutorials/published: GET

## 2023-01-16 - Test the APIs

- How to from:  
  <https://terminalcheatsheet.com/guides/curl-rest-api>
- Start server: `node server.js`
- Open another terminal and ...

### Create a few tutorials using `POST` & `/tutorials` API

```
curl -X POST -H 'Content-Type: application/json' -d '{"title": "Board Games: Tut #1","description": "How to cheat at checkers"}' http://localhost:8080/api/tutorials

curl -X POST -H 'Content-Type: application/json' -d '{"title": "Board Games: Tut #2","description": "How to cheat at chess"}' http://localhost:8080/api/tutorials

curl -X POST -H 'Content-Type: application/json' -d '{"title": "Pencil & Paper Games: Tut #3","description": "How to cheat at tic-tac-toe"}' http://localhost:8080/api/tutorials

curl -X POST -H 'Content-Type: application/json' -d '{"title": "Delete Me: Tut #4","description": "Nothing here"}' http://localhost:8080/api/tutorials
```

---

### Confirm tutorials were added to testdb using `mysql`

```
$ mysql -u root -p
mysql> USE testdb;
mysql> select * from tutorials;
...
```

---

### Retrieve all Tutorials using `GET` & `/tutorials` API

- curl defaults to `GET` request  
  `curl http://localhost:8080/api/tutorials`

---

### Retrieve a single Tutorial by `id` using `GET` & `/tutorials/<id>` API

- curl defaults to `GET` request  
  `curl http://localhost:8080/api/tutorials/2`

---

### Update a Tutorial using `PUT` & `/tutorials/<id>` API

```
curl -X PUT -H 'Content-Type: application/json' -d '{"description": "How to lose at checkers"}' http://localhost:8080/api/tutorials/1

curl -X PUT -H 'Content-Type: application/json' -d '{"description": "How to lose at chess"}' http://localhost:8080/api/tutorials/2

curl -X PUT -H 'Content-Type: application/json' -d '{"description": "How to lose at tic-tac-toe"}' http://localhost:8080/api/tutorials/3

curl -X PUT -H 'Content-Type: application/json' -d '{"published": true}' http://localhost:8080/api/tutorials/3
```

---

### Find all Tutorials, where title contains "board"

#### `GET` & `/tutorials?title=board`

- `curl http://localhost:8080/api/tutorials?title=board`

---

### Find all published tutorials using `GET` & `/tutorials/published` API

- `curl http://localhost:8080/api/tutorials/published`

---

### Delete a Tutorial using `DELETE` & `/tutorials/<id>` API

- `curl -X DELETE http://localhost:8080/api/tutorials/4`

---

### Delete all Tutorials using `DELETE` & `/tutorials` API

- `curl -X DELETE http://localhost:8080/api/tutorials`

---
