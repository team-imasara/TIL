# NodeJS Quickstart Cheatsheet

## Initial Setup
1.  `npm init` in directory
2. Enter info on prompt...
    - "Test command"?
3. `touch server.js` for server protocols
4. `mkdir api` for api directory
    - `mkdir api/controllers api/models api/routes` to set up each directory
5. `touch api/controllers/<name>Controller.js api/models/<name>Model.js api/routes/<name>Routes.js`
    - Replace `<name>`  with stuff

## Install express and nodmon

1. `npm install --save-dev nodemon` nodmon: helps development by watching changed files
2. `npm install express --save` create server using express
3. in `package.json`  add  `"start": "nodemon server.js"` under "scripts"
4. in `server.js`

```
var express = require('express'),
  app = express(),
  port = process.env.PORT || 3000;

app.listen(port);

console.log('todo list RESTful API server started on: ' + port);
```

## as API
[node.js - Proper way to return JSON using node or Express - Stack Overflow](https://stackoverflow.com/questions/19696240/proper-way-to-return-json-using-node-or-express)
```
    response.setHeader('Content-Type', 'application/json');
    response.send(JSON.stringify({ a: 1 }));
```
[javascript - Returning Json with nodeJS - Stack Overflow](https://stackoverflow.com/questions/35601058/returning-json-with-nodejs)


## With MySQL

`npm install mysql`

- [MySQL with Node.js - Stack Overflow](https://stackoverflow.com/questions/5818312/mysql-with-node-js)
- [How To Use MySQL With Node & Express](https://www.terlici.com/2015/08/13/mysql-node-express.html)

### Using `nodejs-mysql`

```
// setup
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'example.org',
  user     : 'bob',
  password : 'secret',
});

connection.connect(function(err) {
  // connected! (unless `err` is set)
});
```

Queries:

```
var post  = {id: 1, title: 'Hello MySQL'};
var query = connection.query('INSERT INTO posts SET ?', post, function(err, result) {
  // Neat!
});
console.log(query.sql); // INSERT INTO posts SET `id` = 1, `title` = 'Hello MySQL'
```

Read & Write to MySQL

```
var mysql = require('mysql')

var connection = mysql.createConnection({
  host: 'localhost',
  user: 'your_user',
  password: 'some_secret',
  database: 'the_app_database'
})

connection.connect(function(err) {
  if (err) throw err
  console.log('You are now connected...')

  connection.query('CREATE TABLE people(id int primary key, name varchar(255), age int, address text)', function(err, result) {
    if (err) throw err
    connection.query('INSERT INTO people (name, age, address) VALUES (?, ?, ?)', ['Larry', '41', 'California, USA'], function(err, result) {
      if (err) throw err
      connection.query('SELECT * FROM people', function(err, results) {
        if (err) throw err
        console.log(results[0].id)
        console.log(results[0].name)
        console.log(results[0].age)
        console.log(results[0].address)
      })
    })
  })
})
```
