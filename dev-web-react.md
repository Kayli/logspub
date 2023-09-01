# notes related to react development

## basics

- ui is a function of the state and properties


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


## reactrouter

- key elements
  - Routes
  - Route
  - BrowserRouter
  - Outlet
  - Link, NavLink


## useful components

- mui: intuitive react ui tools
- react testing
- formik: react forms
- rtk-query: data fetching and caching tool
  - is a part of redux optional extensions


## other

- useParams() function allows to access querystring parameters of the page
