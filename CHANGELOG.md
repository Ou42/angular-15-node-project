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

## 2023-01-16 - Angular 15 Front-end

### Setup Angular 15 Project

- Installed Angular
  - Angular requires an "active LTS" version of Node.js  
    per: <https://angular.io/guide/setup-local>
  - set `nvm` default to `lts/hydrogen`  
    `$ nvm alias default lts/hydrogen`  
    now it defaults to v18.13.0
  - `$ npm install -g @angular/cli`
- Created new Angular Project
  - `$ ng new angular-15-crud-example`
  - ? Would you like to add Angular routing? Yes
  - ? Which stylesheet format would you like to use? CSS
- Generate Components and Services
  - `$ ng g s services/tutorial`
  - `$ ng g c components/add-tutorial`
  - `$ ng g c components/tutorial-details`
  - `$ ng g c components/tutorials-list`
  - `$ ng g class models/tutorial --type=model`

### Setup App Module

- imported `FormsModule` & `HttpClientModule`  
  to app.module.ts

### Define Routes for Angular AppRoutingModule

> There are 3 main routes:
> - /tutorials for tutorials-list component
> - /tutorials/:id for tutorial-details component
> - /add for add-tutorial component

### Define Model Class

- export main model class `Tutorial`
- found in *tutorial.model.ts*
- contains 4 fields:
  - id
  - title
  - description
  - published

### Create Data Service

- *services/tutorial.service.ts*
- ... uses Angular HttpClient to send HTTP requests
- > functions include CRUD operations and finder method.

## 2023-01-16 - Continue with step by step

- Links to another tut:
  - Angular 15 example: CRUD App with Web API
  - <https://www.bezkoder.com/angular-15-crud-example/>

### Import Bootstrap into Angular 15 Project

- `npm install bootstrap@4.6.2`
- edit *src/style.css* & import bootstrap

### Add Navbar & Router View

- *src/app.component.html*
  - is an `App` component
  - is the root container of the application
- add `nav` element

## 2023-01-17 - Create Angular 15 Components

- 3 components correspond to 3 routes defined in `AppRoutingModule`

### Add new Item Component

- Create a Form to submit new Tutorial with 2 fields:  
  `title` & `description`.
- It calls `TutorialService.create()` method.
- update:
  - *components/add-tutorial/add-tutorial.component.ts*
  - *components/add-tutorial/add-tutorial.component.html*
  - *components/add-tutorial/add-tutorial.component.css*

## 2023-01-23 - Create Angular 15 Components

- 3 components correspond to 3 routes defined in `AppRoutingModule`

### List of items Component

- WIP

## 2023-02-09 - Moved local SQL server to a container

- using podman, a docker alt
- `$ podman pull mysql:8-debian`
- `$ podman run --name my-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<secret> -v $HOME/mysql-data:/var/lib/mysql -d mysql:8-debian`
- replace \<secret\> w/ actual MySQL root password

### ***IF*** the container already exists

- If `$ podman ps -a` lists the container
- then, `$ podman start my-mysql`
- start the node server: `$ node server.js`
- open a new terminal
- use `curl` for CRUD ops ( see above )
- return to previous terminal
- Ctrl + c to stop node server
- `$ podman stop my-mysql` to stop the container
