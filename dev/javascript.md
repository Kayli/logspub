# notes related to javascript and typescript

## basics

- var, let, const
  - let is more strict than var
    - scoped to a block
    - not added to global object ('window' in browsers)
  - avoid using var
  - always use const by default, unless you need let or var

- imports
  - commonjs
      - uses require() to load modules
      - module.exports = { <list of modules> }

  - es6 modules
    - gained wide support by 2020 in major modern browsers
    - import statement
    - export statement
      - exports multiple items, names should be the same when importing
      - you can have multiple export statements in a module
        - export <item>;
      - or you can list all items in a single statement
        - export { <item1>, <item2> };
      - export default <item>;
        - exports only a single item
        - allows to specify any name when importing
    - syncroniously loaded by default
    - import() can be called as a function and it returns a promise
    - need to have type="module" attribute in the script tag of the package.json to work
    - can't be used on files on local machine due to cors

- string interpolation
  - use backticks `something ${myVar}`

- async programming
  - Promise: supports callbacks and chaining
  - async/await
    - functions defined with 'async' always return a Promise
      - and the value of that Promise will be whatever the async function returns
    - you can then await such function to yield result
      - or you can also await a promise

- json: JSON.parse(), JSON.stringify()


## this binding

- 'this' is dynamically bounded depending on the calling context
  - example
    ```javascript
      function Person(name) {
        this.name = name;
        this.sayName = function() {
          setTimeout(function() {
            console.log(this.name); // `this` refers to the global object, not the Person instance
          }, 1000);
        };
      }
    ```

- to explicitly bind 'this', use 'call' function of a function object
  ```javascript
    const person = { name: 'vasya' };
    function sayHello() {
      console.log(`Hello, my name is ${this.name}`);
    }
    sayHello.call(person);
  ```

- arrow functions
  - examples
    ```javascript
      const myFunc1 = x => 5;
      const myFunc2 = (x, y) => 7;
      const myFunc3 = x => { console.log('test'); };
    ```
  - capture 'this' value from the surrounding lexical scope at the time they are defined



## working with dom

- single element selector: document.querySelector('.myclass')
- multiple elements selector:  document.querySelectorAll('.myclass')


## oop

- constructor functions
  ```javascript
    function Person(name, age) {
      this.name = name;
      this.age = age;
      this.sayHello = function() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
      }
    }
    const person1 = new Person('Alice', 30);
    const person2 = new Person('Bob', 25);
  ```

- prototypes
  ```javascript
    function Person(name, age) {
      this.name = name;
    }
    Person.prototype.sayHello = function() {
      console.log(`Hello, my name is ${this.name}`);
    }
  ```

- classes
  - are syntactic sugar around constructor functions and prototypes
  ```javascript
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }
      sayHello() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
      }
    }
  ```


## event loop

- task queue
  - functions like setTimeout, setInterval add callback function to a task queue
  - when stack is empty, js runtime will pick next item from the task queue

- microtask queue: for code to be executed after await of the async function
  - has priority over the task queue
    - so runtime will process all items in microtask queue before running anything else
  - if that code causes another microtask to be created - we'll get stuck in infinite loop
  - callbacks for promises will also go to a microtask queue
    ```javascript
    Promise.resolve().then(() => {
      console.log("Resolved")
    })
    ```

- both task queue and microtask queue are fifo queues


## nodejs [1]

- global namespace objects and functions
  - global: similar to window in browser
  - process
    - process.argv: command line parameters
    - process.env: environment variables
  - setTimeout, setInterval

- useful libraries
  - nodemon: autowatch source files and restrart node server on change
  - express: web server framework

## references

[1]: https://www.youtube.com/watch?v=32M1al-Y6Ag (nodejs crash course 2024)
[2]: https://www.youtube.com/watch?v=CnH3kAXSrmU (expressjs crash course 2024)