# nodejs-made-easy

This is a comprehensive and up-to-date Node.js course for JavaScript back-end developers

## Getting Started

[Home](../README.md) / [What is node](./what-is-node.md) / First Node program

![Picture](../images/node-download.png)

### Installation

- Check if node is already installed on your machine or not

  ```sh
  $ node --version
  v18.12.1
  ```

- if not, download the recommended latest stable version from [Node JS homepage website](https://nodejs.org/en/)

### First Node program

- ctrate a file and write tour first node program inside it

  ```js
  function sayHello(name) {
    console.log("Hello " + name);
  }

  sayHello("Jose");
  ```

- open the ternimal, run a node and passing a name of a file as an argument

  ```zsh
  $ node 1-getting-started/hello.js
  Hello Jose
  ```
