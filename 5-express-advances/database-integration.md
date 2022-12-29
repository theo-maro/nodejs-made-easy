# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## Express - Advanced Concepts

In this section, will look more advanced concepts like middleware, configuration, debugging, template engine and more...

[Home](../README.md) / [Middleware](./middleware.md) / [Configuration](./configuration.md) / [Debugging](./debugging.md) / [Template Engine](./template-engines.md) / Database Integration

### Database Integration

Adding the capbility to connect databases to Express apps is just a matter of loading an appropriate Node.js driver for the database in your app.

#### Integrating MongoDB

##### How to work with MongoDB

- Install the `mongodb` driver

  ```zsh
  $ npm install mongodb
  ```

- load the mongodb module

  ```js
  import { MongoClient } from "mongodb";
  ```

- Access various collections

  ```js
  MongoClient.connect("mongodb://localhost:27017/animals", function (err, db) {
    if (err) throw err;

    db.collection("mammals")
      .find()
      .toArray(function (err, results) {
        if (err) throw err;
        console.log(results);
      });
  });
  ```

##### Work with Mongoose

<!-- TODO -->

- Install the `mongoose` driver

  ```zsh
  $ npm install mongoose
  ```

- load the mongoose module

  ```js
  import {} from "mongoose";
  ```

- Access various collections

  ```js
  //
  ```

#### Integrating MySQL

<!-- TODO -->
