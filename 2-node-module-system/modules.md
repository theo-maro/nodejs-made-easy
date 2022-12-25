# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## Node Module System

In this section, we're going to look at module system in Node by exploring the common modules built-in of the core such as `fs`, `os`, `events`, and `http` etc. you'll learn

- What modules are?
- Why we need them?
- How do they work?
- how to create custom modules?

### Modules

At the core of Node, we have this concept called `module`.

- Every file in a node application is considered a module.

  ```js
  console.log(module)

  // output
  Module {
  id: '.',
  path: '/home/jm/Documents/GitHub/nodejs-made-easy/2-node-module-system',
  exports: {},
  filename: '/home/jm/Documents/GitHub/nodejs-made-easy/2-node-module-system/globals.js',
  loaded: false,
  children: [],
  paths: [
      '/home/jm/Documents/GitHub/nodejs-made-easy/2-node-module-system/node_modules',
      '/home/jm/Documents/GitHub/nodejs-made-easy/node_modules',
      '/home/jm/Documents/GitHub/node_modules',
      '/home/jm/Documents/node_modules',
      '/home/jm/node_modules',
      '/home/node_modules',
      '/node_modules'
  ]
  }
  ```

#### Creating a Module

To create a module in node, simply create a new file in your project folder

- The variable and functions defined in that module/file are private i.e. only scoped to that file.

- To use a variable or function defined inside a module, must explicitly export it and make it public

- `NOTE`: we may sometimes export an object of multiple properties and methods

  ```js
  // logger.js

  function log(message) {}

  module.exports.log = log; // exporting function
  module.exports.url = this.url; // exporting variable
  ```

- `NOTE`: Or we may instead export only a single function

  ```js
  // logger.js

  function log() {}

  module.exports = log;
  ```

#### Loading a Module

- To load a module somewhere else in our node application we use `require()` function.
- This `require()` function returns the object that is exported by a target module

- `NOTE`: as the best practice, store the results in constant to prevent accidentally override the value of loaded module.

  ```js
  // app.js

  const logger = require("./logger.js");

  logger.log("This is a message");
  ```

- loading a function from a target module instead of an object

  ```js
  const log = require("./logger.js");

  log("This is a message");
  ```

#### Module Wrapper Function

- Node does not execute the codes inside a module directly, instead it wrap them inside a module wrapper function (IEFE).

  - with this function, require function, module, exports are local to each module
  - filename, and dirname represent the name of each module and the path

    ```js
    (function (exports, require, module, __filename, __dirname) {
      function wrapper() {}

      module.exports.wrapper = wrapper;
    });
    ```
