# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## Node Package Manager

[NPM](https://www.npmjs.com) is basically a command-line tool as well as a registry of third-party libraries we can add to our node applications.

[Home](../README.md) / NPM Packages / [Semantic Versioning](./semantic-versioning.md) / [Publishing Packages](./publish-package.md)

### Working with Local Packages

- The way we add those node modules to our application is via command-line tool called `npm` which ship along with node

  - Check if npm is installed

  ```zsh
    $ npm -v
  ```

  - Install npm globally (specific version)

  ```zsh
    $ sudo npm i -g npm@8.19.2
  ```

#### Package.json file

- This is a json file that include basic information(metadata) about your project/application such as its name, version number, authors, address of its git reposiory, its dependancies and so on.

- `NOTE`: Before adding any node packages to your application, you need to create package.json file

  - Initializing the project folder and add package.json file

  ```zsh
  $ npm init -y
  ```

#### Install and Use a Local Package

- install a third-partly libraries to your node application

  ```zsh
  $ npm i underscore
  ```

- load and use an installed package to your node application

  ```js
  // load a module
  const _ = require("underscore");

  // use a module
  var result = _.contains([1, 2, 3, 4], 2);
  console.log(result);
  ```

#### Uninstall Local Packages

- Remove a no longer required package from a node application

  ```zsh
  $ npm un underscore
  ```

### Working with Global Packages

These global packages are not specific to a node application and we can access them from anywhere

- To install global package simply add `-g` flag

  ```zsh
  $ npm i -g uuid
  ```

- To uninstall global package simply add `-g` flag

  ```zsh
  $ npm un -g uuid
  ```

- All other commands work the same as a local packages

### Node Package Dependencies

#### Application Dependencies

Application dependancies are all package dependancies that our application needs in order to function properly.

- When install a node package, that package may ship with other packages that it depend upon.

- install appDependencies

  ```zsh
  $ npm i jshint --save-dev
  ```

- In package.json

  ```json
  {
    "dependencies": {
      "mongoose": "^6.8.1"
    }
  }
  ```

#### Development Dependencies

Development dependancies are those packages that only used during development such as running unit test.

- They should not go into production enviroment where we deploy our application

- install devDependencies

```zsh
$ npm i jshint --save-dev
```

- In package.json

```json
{
  "devDependencies": {
    "jshint": "^1.13.6"
  }
}
```

### Exclude Packages from SCM

All of our application dependencies are stored inside a package.json file

- We can easily restore these version of these dependencies on any machine

  - NPM will look at package.json file and it will download and install those dependencies for us

    ```zsh
    $ npm install
    ```

- `NOTE`: As the best practice we should exclude the node modules folder from our source control repositories

  - using git, add .gitignore file from which will list all files and folder to be excluded
