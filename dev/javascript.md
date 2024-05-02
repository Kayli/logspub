# notes related to javascript and typescript

## basics

- var vs let: let is more strict
  - scoped to a block
  - not added to global object ('window' in browsers)

- imports
  - commonjs
      - uses require() to load modules
      - module.exports = { <list of modules> }

  - es6 modules
    - gained wide support by 2020 in major modern browsers
    - import and export statements
    - syncroniously loaded by default
    - import() can be called as a function and it returns a promise
    - need to have type="module" attribute in the script tag to work
    - can't be used on files due to cors

- async programming
  - Promise: supports callbacks and chaining
  - async/await
    - functions defined with 'async' always return a Promise
      - and the value of that Promise will be whatever the async function returns
    - you can then await such function to yield result
      - or you can also await a promise
