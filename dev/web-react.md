# notes related to react development

## basics

- ui is a function of the state and properties

- core concepts
  - components
    - reusable piece of ui
    - function returning a markup with only one root element

  - hooks
    - useState: creates a state variable with mutation/setter function for that state
    - useEffect: tell react that your component needs to do something after render
    - useParams: reactrouter hook that returns page url parameters

  - jsx

- create new react app
  > npm create vite@latest <name>
  > npm install
  > npm run dev


## state management

- redux (advancement over flux)
  - ideomatically functional
  - state transformations are more explicit, therefore more transparent?
  - enables "time-travel debugging" and provides additional debugging tools 
  - more boilerplate
    - as it explicitly defines 'actions' (which are actually event dtos)
    - and then suggests to wrap them in constructor functions 
      - or to write a constructor function generator ... yeah, very cool

- mobx
  - is available for react as well
  - implements oop stype observables, similar to knockout.js
  - supports linting: verify your coding patterns at runtime by hinting at smells
  - main principles
    - uses uni-directional data flow: actions change the state, state updates all affected views
    - all computed values should be pure. They are not supposed to change state
  - there are time-travel debugging addon libraries as well
  - some pros and cons: https://dzone.com/articles/drawbacks-of-mobx

- apollo: state management and graphql framework
  - https://www.apollographql.com/docs/react/get-started

- hooks and observables
  - https://nils-mehlhorn.de/posts/react-hooks-rxjs/
    - https://github.com/streamich/react-use
    - https://github.com/LeetCode-OpenSource/rxjs-hooks
    - https://github.com/crimx/observable-hooks


## reactrouter

- key elements
  - Routes
  - Route
  - BrowserRouter
  - Outlet
  - Link, NavLink

- to preserve DOM elements between different routes use ReactDOM.createPortal
  - ask chatgpt for more


## useful components/tools

- react developer tools: chrome extension
- vite: initial scaffolding
- react query: simplifying fetch in react

- mui: intuitive react ui tools
- react testing
- formik: react forms
- rtk-query: data fetching and caching tool
  - is a part of redux optional extensions


## other

- useParams() function allows to access querystring parameters of the page
