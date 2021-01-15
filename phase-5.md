### Phase 5

- [Redux Intro](#intro)
- [Redux and React](#react-and-redux)
- [Redux Thunk](#thunk)

## Lecture Notes

---
title: Redux Intro
layout: post
---

# <a id="intro">Introduction to Redux</a>

No setup required for this lecture, it is presentation accompanied by a slideshow. The overaching goal of this lecture is to introduce students to the Redux library and explain why we want to use it within our applications.


## SWBATs
* Give a general outline of Redux. What is Redux and what does it do for us?
* Show how state is managed through Redux and how the store works.
* Explain the problems that come with everchaning state in React.
* Explain why Redux is a solution to React state problems.



## Resources
* [Redux Lecture Slides](https://docs.google.com/presentation/d/1IIzo1y-nHkQEGtEhDiq7NevbTipq0jGj9XjOs4hLE9Q/edit#slide=id.g342b7ede26_0_19)

## Outline



```
   5m | Problems of React
   5m | The Solution: Redux
  10m | Single Source of Truth: Store
  10m | Read and Writing to the Store
  10m | Pure Functions: Reducers
  10m | Unidirectional Flow
   5m | Common Hurdles of Redux
   5m | Questions
  ----|----
  60m Total
```

### Problems of React
* State is ever-changing and is constantly being mutated in React.
* Large React apps require props to be passed needlessly throughout the component tree.
* React apps with tons of stateful components are constantly rerendering.

### The Solution: Redux
* What Is Redux?
  * The goal of Redux is to make state **global** and make all state changes **predictable**
  * Redux at its core is a state manager built for React.js 
  * The main concept behind Redux is to store state in a central location and allow each component to access that state without having to send props down to child components or use callback functions to send data back up to the parent

* Why Redux?
  * As your React applications become increasingly more complex, State becomes increasingly harder to manage 
  * An app with 20+ stateful components in its structure ignores the single source of truth principle and changes in state are difficult to track
  * Redux alleviates these issues by placing state in a single, central location that all of your components can interact with

### Single Source of Truth
* We use the Redux store to contain a singular and universal state within our application.
* Redux Store
  * The Redux store is a plain JS object that exposes a few Redux specific methods like `dispatch` and `getState`. Our applications state lives here
  * The store is created at the very beginning of an application with the `createStore` function

### Reading and Writing to the Store
* With Redux, the state of our application will actually never *change*. Instead, the `store` is alerted of changes and returns a new state based off of the previous state and incoming alterations.
* The state can be accessed by the method `getState`, a reader method
* The state can be manipulated by sending an "action" to a method called `dispatch`
  * An action is a plain object containing the instructions and information that describes the state changes we expect to see
  * Actions typically have two keys: 
    * `type`: a string used to identify the type of state change
    * `payload`: any data needed to complete the state change

### Pure Functions: Reducers
* When we get an action telling us how the state should change, we use pure functions called reducers that do not mutate state but instead return an entirely new state to replace the old one
* Reducers
  * A reducer function's job is to read an action and return newly updated state
  * When a Redux store is created via `createStore`, the reducer is given as its first argument
  * A reducer function receives two arguments: the current state and an `action` object
  * The return value of the reducer function will become the new state
  * An easy way to remember the role of a reducer is that it takes two arguments and _reduces_ them to one thing, the new state

### Unidirectional Flow
* Manipulating the Redux store can be broken down to a series of unidirectional steps
  1. Component triggers an action
  2. Action sent to reducer
  3. Reducer returns the new state
  4. Change in store causes rerender in components that rely on the piece of state that changed
  
### Common Hurdles of Redux
* Global State:
  - Students often struggled with understanding that their applications state now exists in one, solitary location. Previously, state existed in multiple locations and students were comfortable constructing stateful components. At first, it may seem odd for them to relocate every piece of their state to one place.
* Reducers: 
  - Students have difficulty understanding the role of reducers in their application and why we need them. The main role of a reducer is to interpret dispatched messages and tell the store to return a new version state.

  ---
title: Redux And React
layout: post
---

# <a id="react-and-redux">React to Redux</a>

## SWBATs

* Transform a React application with local state inside the Container Component to a React-Redux application with state held in the store
* Walk through implementing the `redux` and `react-redux` libraries
* Convert a function passed down as a prop to a child component into an action that will hit a `switch` case inside a `rootReducer`
* Update `state` inside the redux store through an action that is dispatched to the reducer

## Resources

* [React to Redux](https://youtu.be/tMjM8yT15GU)

## Outline

    10m React App Walk Through
     5m Implement Redux and React-Redux Libraries
    10m Hold State Inside Store
    15m Create Actions and Reducers
    20m Update State Inside Redux Store
    15m Breakout
    ===
    75m Total

### React App Walk Through

Take this time to show how the application functions in the browser. It is ideal to have state held locally inside of a `Container` component that App renders. Then, have a `List` component that has state passed down as props. In the `List` component, iterate over the objects in state to load a single list item in a `Detail` component.

Students usually have a hard time grasping the core of redux and will get lost in all the set up that needs to take place. Emphasize that a majority of the code to implement Redux is predominately boilerplate and keep the React app simple so that they can focus on Redux portion. If there is a domain that the students are familiar with from previous lectures or review sessions, bring those up as examples and explain how Redux would allow them to access information without passing it down as a prop through multiple components.

##### React App Component Hierarchy
* App
* Container
  - In here, pass down all local state as a prop to `List`
* List
  - Iterate through all of the items inside of props and pass a single item to the `Detail` component
* Detail

##### React App Local State

`State` in the `Container` component should point to an object with a key of some type of attribute, such as `instructors`. In this application, is ideal to have one key inside the `instructor` object point to an integer, such as a `votes` key that points to `0`. There can be another key that points to a `boolean`, such as a `inNYC` key that returns a `boolean` value depending on if that instructor currently teaches in Manhattan.

```js
  state = {
    instructors: {
      one: { id: 'one', name: 'Steven', age: 100, votes: 0, inNYC: true },
      two: { id: 'two', name: 'Niky', age: 101, votes: 0, inNYC: false },
      three: { id: 'three', name: 'Tim', age: 102, votes: 0, inNYC: false }
    }
  }
```

##### React App Functionality

* Create an `upVote` and `downVote` function that will use `this.setState` to either increment or decrement the votes for that `instructor` and update state inside the `Container` component

* Pass the `upVote` and `downVote` functions as a prop to the `List` component

```
class Container extends Component {
  state = {
    instructors: {
      one: { ... },
      two: { ... },
      three: { ... }
    }
  }

  upVote = instructorId => {
    this.setState({
      instructors: {
        ...this.state.instructors,
        [instructorId]: {
          ...this.state.instructors[instructorId],
          votes: this.state.instructors[instructorId].votes + 1
        }
      }
    })
  }

  downVote = instructorId => {
    this.setState({
      instructors: {
        ...this.state.instructors,
        [instructorId]: {
          ...this.state.instructors[instructorId],
          votes: this.state.instructors[instructorId].votes - 1
        }
      }
    })
  }

  render() {
    return (
      <div>
        <List instructors={this.state.instructors} upVote={this.upVote} downVote={this.downVote} />
      </div>
    )
  }
}

export default Container;
```

* Iterate over the props inside the `List` component and render a `Detail` component for each `instructor` object

* Display all of the features of each `instructor` in the `Detail` component

* Create a `+` and `-` button that will invoke the `upVote` or `downVote` function, which will invoke the `upVote` function passed down as a prop with the `instructor.id` as an argument and update state in the `Container` component

```js
  const upVote = () => {
    props.upVote(props.instructor.id);
  }

  const downVote = () => {
    props.downVote(props.instructor.id);
  }
```

* Reiterate that state should not be directly mutated and `this.setState` should instead use the spread operator

### Implement Redux and React-Redux Libraries

* Install and save the `react-redux` and `redux` libraries into the application

* In `index.js`, import the `Provider` from `react-redux` and `createStore` function from `redux`

* Create the store by invoking the `createStore` function and saving it to a variable, i.e. `store`

* `Console.log` the store inside `index.js` and go inside the Developers Console inside the browser and show the functions provided with the store

* Pass the `store` to the `<Provider />` as a prop and then wrap the `<App />` inside the `<Provider />`

### Hold State Inside Store

The students now need to understand that state is changing from being accessible inside every component as long as you pass it down as a prop. Now, instead of passing state down a lot of components, we will have it inside the store. The store can be explained as the gatekeeper, so to speak, that will only allow a component to access state if it requests it from the store through redux.

* Create a `reducer.js` file in the `src` folder that exports the `rootReducer` function. Separate reducers can be introduced later

*
```js
export function rootReducer(state = defaultState, action){
    switch(action.type) {
      default:
        return state;
    }
}
```

* Move the local state from the `Container` component into the `reducer.js` and save it to a `defaultState` variable. Add in a `console.log` after `store` is logged in `App.js` to log what the state is by `store.getState()`

* At this point, the application will break because state is no longer passed down as a prop but show that state is exactly the same, just held in a different location

* The `List` component no longer takes `instructors` from state as a prop and can be rendered without any props inside the `Container` component

##### Mapping State to Props

* Inside the `List` component, import `connect` from `react-redux`

* Invoke the `mapStateToProps` function so that instructors can still be referenced as a prop, but as a prop from state inside store

*
```js
const mapStateToProps = state => {
    return {
      instructors: instructors
    }
}
```
* Export the `List` component as connected with the store and to include `mapStateToProps`

* ```js
export default connect(mapStateToProps)(List);
```

### Create Actions and Reducers

Now that state is held inside of the store, the `upVote` and `downVote` functions that update state will need to update state in the `reducer.js` instead. Just like how the previous sections shows that state doesn't change, just the way we access it, the time taken to create these should also include an explanation that an reducer will update the state based on whatever action type we send it.

* Create two actions in an `actions.js` file inside the `src` folder that will take in the `instructorId` so the reducer will know which instructor's votes to update based on the original functionality of the `upVote` and `downVote`

*
```js
export let upVote = instructorId => {
    return {
      type: "INCREASE_VOTE",
      payload: {
        instructorId: instructorId
      }
    }
}
```
```js
export let downVote = instructorId => {
    return {
      type: "DECREASE_VOTE",
      payload: {
        instructorId: instructorId
      }
    }
}
```
* Since there are now different payload types, the `rootReducer` in `reducer.js` will need to account for these in the `switch` statement

*
```js
export let upVote = instructorId => {
    return {
      type: "INCREASE_VOTE",
      payload: {
        instructorId: instructorId
      }
    }
}
```
```js
export function rootReducer(state = defaultState, action){
    switch(action.type) {
      case 'INCREASE_VOTE':
        return {...state,
           instructors: {
             ...state.instructors,
              [action.payload.instructorId]: {
                ...state.instructors[action.payload.instructorId],
                votes: state.instructors[action.payload.instructorId].votes + 1
              }
            }
          }
      case 'DECREASE_VOTE':
        return {...state,
          instructors: {
              ...state.instructors,
              [action.payload.instructorId]: {
                ...state.instructors[action.payload.instructorId],
                votes: state.instructors[action.payload.instructorId].votes - 1
              }
            }
          }
      default:
        return state;
    }
}
```

###Update State Inside Redux Store

Now that our actions have been created, they need to be integrated into the components that will be updating and/or referencing state inside of the store. Again, much of this is boilerplate and should be reiterated as such to the students.

* Import both the `upVote` and `downVote` functions from the `actions.js` file as well as `connect` from `react-redux` into the `Detail` component

* The payload of the action can only be sent to the reducer through dispatch, so the `Detail` component will need to include the `mapDispatchToProps` function as well

*
```js
const mapDispatchToProps = dispatch => {
   return {
    dispatchUpVote: id => dispatch(upVote(id)),
    dispatchDownVote: id => dispatch(downVote(id))
   }
}
```

* Now that we've `mapDispatchToProps`, update the invocation inside the local `upVote` and `downVote` in the `Detail` to now dispatch the action to the reducer with the `instructorId` instead of invoking a function that was passed down as a prop from a parent component

*
```js
const upVote = () => {
   props.dispatchUpVote(props.instructor.id)
}
```
```js
const downVote = () => {
   props.dispatchDownVote(props.instructor.id)
}
```
* Connect the `Detail` component on export and pass it `mapDispatchToProps` as the second argument of the function invocation

*
```js
export default connect(null, mapDispatchToProps)(Detail)
```

###Breakout

* Have students try to create an action and accompanying switch case inside the `rootReducer` to toggle the boolean value of whether or not an `instructor` is `inNYC` or not based on a button being clicked

* In the last five minutes of lecture, there can be a review where the instructor is the driver and the students navigate how this functionality would be implemented with redux

---
title: Redux Thunk
layout: post
---

# <a id="thunk">Async Redux with Thunk</a>

## SWBATs

* Implement React app with Redux from the ground up
* Navigate the Redux developer tools to visualize Redux store
* Describe why actions can't return objects for async operations
* Explain how Thunk facilitates async action dispatching
* Define middleware
* Explain why it's useful to have a `FETCHING_` and a `FETCHED_` action type

## Resources

* [Example Video](https://www.youtube.com/watch?v=8CqVidHJOO0)

## Outline

    15m Build Basic React App with Redux
    15m Add `fetch` to Application
    10m Apply `thunk` Middleware
    20m Bringing it All Together
    ===
    60m Total

### Build Basic React App with Redux

### Add `fetch` to Application

### Apply `thunk` Middleware

### Bringing it All Together
