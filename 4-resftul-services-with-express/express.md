# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## RESTful Services with Express

Express is a fast and lightweight framework for building web applications

[Home](../README.md) / [RESTful Services](./restful.md) / Express Web Server / [Handling HTTP Requests](./handling-requests.md)

### Introducing Express

The Express framework gives our application a proper structure, so we can easily add more routes while keep our application code maintanable.

- To install Express, run this command

  ```zsh
  $ npm i express
  ```

- the express app object has bunch of methods that correspond to http methods

  ```js
  app.get(); // for handling http GET request
  app.post(); // for handling http POST request
  app.put(); // for handling http PUT request
  app.delete(); // for handling http DELETE request
  ```

#### Enviroment Variables

An enviroment variable is basically a variable that is part of enviroment in which a process runs. Its value is set outside the node application.

- In node applications, we have this enviroment variable called `PORT`. To read it value we use a process object

  ```js
  const PORT = process.env.PORT || 3000;
  ```

#### Route Parameters

Route parameters are parameters added to url after `/:` to provide essential or required values

- get a single parameter

  ```js
  app.get("/api/posts/:id", (req, res) => {
    res.send(req.params);
  });
  ```

  Example url : `localhost:3000/api/posts/1`

- get multiple parameters

  ```js
  app.get("/api/posts/:year/:month", (req, res) => {
    res.send(req.params);
  });
  ```

  Example url : `localhost:3000/api/posts/:2022/:10`

#### Query Strings

Query strings are params added to url after `?` to provide optional data for our backend services

- get a query string

  ```js
  app.get("/api/posts/:2022/:8", (req, res) => {
    res.send(req.query);
  });
  ```

  Example url : `localhost:3000/api/posts/:2022/:10?sortBy=date_created`

### Building First Express Web Server

- load an express module in your app

  ```js
  const express = require("express");
  const app = express();
  ```

- define a routes/endpoints

  ```js
  app.get("/", (req, res) => {
    res.send("Hello world");
  });

  app.get("/api/users", (req, res) => {
    res.send([
      { id: 1, uname: "josMe" },
      { id: 2, uname: "amJ" },
      { id: 3, uname: "Theo" },
    ]);
  });
  ```

- listen at a given port

  ```js
  const PORT = process.env.PORT || 3000;
  app.listen(PORT, () => {
    console.log(`Listening at port ${PORT}...`);
  });
  ```
