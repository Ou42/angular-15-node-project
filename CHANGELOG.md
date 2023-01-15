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
- [ ] findAll
- [ ] findOne
- [ ] update
- [ ] delete
- [ ] deleteAll
- [ ] findAllPublished
