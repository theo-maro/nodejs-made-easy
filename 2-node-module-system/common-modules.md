# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## Node Module System

In this section, we're going to look at module system in Node by exploring the common modules built-in of the core such as `fs`, `os`, `events`, and `http` etc.

[Home](../README.md) / [Global Object](./global-object.md) / [Module](./modules.md) / Built-in Module

### Built-in Modules

- Node comes with useful modules that are built into the core of Node. With these modules we can work with files, operating system, network and so on.

#### Path Module

- Gives us a bunch of utility functions for working with files and directory paths. It can be accessed using:

  ```js
  const path = require("path");

  var pathObj = path.parse(__filename);

  console.log(pathObj);
  console.log(pathObj.root);
  console.log(pathObj.dir);
  console.log(pathObj.name);
  console.log(pathObj.ext);
  console.log(pathObj.base);
  ```

#### OS Module

- With these we can work with operating system
- we can get information about current operating system

  ```js
  const os = require("os");

  //
  var platform = os.platform();
  var release = os.release();
  console.log(`Distro : ${release} - ${platform}`);

  // get total and free free amount of memory on machine
  var freeMemory = os.freemem();
  var totalMemory = os.totalmem();
  console.log(`Free : ${freeMemory}  \nTotal : ${totalMemory}`);

  //
  homeDir = os.homedir(); //
  hostName = os.hostname(); //
  console.log(`Host : ${hostName} \nHomeDir : ${homeDir}`);

  // get current user infomation
  user = os.userInfo();
  console.log(`Username : ${user.username} \nHomeDir : ${user.homedir}`);
  ```

#### File System Module

- With these we can work with files and directives.
- Almost every operation defined in this module comes into two(2) forms blocking(sync) or non-blocking(async)

  ```js
  // get all the files and directories in a given path synchronously
  const fs = require("fs");

  const files = fs.readdirSync("./");
  console.log(files);
  ```

- `NOTE`: as the best practice always prefer to use async operations. This is because node process has single thread and it will not keep that thread busy.

  ```js
  // get all the files and directories in a given path asynchronously
  const fs = require("fs");

  fs.readdir("./", function (err, files) {
    if (err) console.log("Error", err);
    else console.log(files);
  });
  ```

#### Process Module

- Gives us information about the current process

  ```js
  const ?? = require("??");
  ```

#### Events Module

- An event is a signal indicates that something has happened. In our Node app we may want to respond to those events. Different classes in node raise different kind of events

  - emit is a method that raise an event while listener is a function that would be called when an event is raised
  - Order matters, that is the listener must be registered first before calling the emit method

    ```js
    const EventEmitter = require("events");

    const emitter = new EventEmitter();

    // register a listener
    emitter.on("messageLogged", () => {
      console.log("Listener called");
    });

    // raise an event
    emitter.emit("messageLogged");
    ```

- Event arguments : allows us to pass data about an event that just happened

  - when raising an event, we might also want to send some data about that event such as message id, url
  - the registered listener can also receive those event arguments

    ```js
    // register a listener with event arguments
    emitter.on("logging", (arg) => {
      console.log(arg.message);
    });

    // raise an event with event arguments
    emitter.emit("logging", { message: "logging an event" });
    ```

- Extending EventEmitter : instead of working with EventEmitter class directly.

  - Instead, we may want to create a new class that extends all the capabilities of EventEmitter

    ```js
    const EventEmitter = require("events");

    class Logger extends EventEmitter {
      log(message) {
        this.emit("messageLogged", { id: 1, url: "http://" });
        console.log(message);
      }
    }

    module.exports = Logger;
    ```

  - accessing an extended Logger class in app.js

    ```js
    const Logger = require("./logger");

    const logger = new Logger();

    logger.on("messageLogged", (arg) => {
      console.log("Listener called at", arg.url);
    });
    logger.log("The message is logged here");
    ```

#### HTTP Module

- Allow us to create server that listen to http requests on a given port. With this we can easily create a backend service for our client app

  - create a http server, this server is an event emitter as it has all the capabilities of EventEmitter class
  - every time there is new connection, this server will raise an event, we use on() method to handle that event

    ```js
    const http = require("http");

    const server = http.createServer();
    const PORT = 3000;

    // register a event listener
    server.on("connection", (socket) => {
      console.log("New connection established...");
    });

    // listen to a connection event raised
    server.listen(PORT);
    console.log(`Listening on port ${PORT}...`);
    ```

    - In real-world applications we're not going to respond to a connection event to build an http service, instead we're going to work with actual response or request to build backend services for our client app by handling various route.

    ```js
    const http = require("http");
    const PORT = 3000;

    const server = http.createServer((req, res) => {
      if (req.url === "/") {
        res.write("Hello World!");
        res.end();
      }
      if (req.url === "/api/courses") {
        res.write(
          JSON.stringify([
            {
              id: 1,
              name: "fullstack web development",
              price: 300,
              duration: "3 weeks",
            },
            {
              id: 2,
              name: "Mobile app development",
              price: 350,
              duration: "3 weeks",
            },
          ])
        );
        res.end();
      }
    });

    // listen to a connection event raised
    server.listen(PORT);
    console.log(`Listening on port ${PORT}...`);
    ```

#### Query Strings

- this is very useful for building http services

  ```js
  const ?? = require("??");
  ```

#### Stream

- this allows us to work with streams of data

  ```js
  const ?? = require("??");
  ```
