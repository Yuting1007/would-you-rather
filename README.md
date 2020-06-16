# Code Notes

### API functions 
getInitialData - takes in _getUsers & _getQuestions

saveQuestion - location to format data for post request

saveQuestionAnswer - location to format data for post request

This is located at */src/utils/api.js*

### Actions
**Actions are payloads of information that send data from your application to your store. They are the only source of information for the store.**

The next step is to create a set of actions and action creators.
This is located at */src/actions/*

### Reducers
**Reducers specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes.**

**The reducer is a pure function that takes the previous state and an action, and returns the next state.**
```
(previousState, action) => nextState
```

The next step is to create our reducers.
This is located at /src/reducers/
*/src/reducers/index.js* is where we combine the reducers into one main root reducer (combine authUser reducer, question reducer and users reducer)

*/src/index.js* we also need to instantiate the redux store and pass it to Provider which warps App and acts as a Context

### Middleware
**It provides a third-party extension point between dispatching an action, and the moment it reaches the reducer.**

This is located at */src/middleware/*
All middleware follows this currying pattern 
```
const logger = (store) => (next) => (action) => {
 // ...
}
```
The first middleware function will be a logger taht will output action and state.

One thing to note is that middleware gets run after the action creator returns an object or function but before getting sent to the reducer.

Middleware also gets run in the order we apply it. Thunk needs to be run first so that it can properly handle logger.

### Initialize App Data
We need to invoke our `handleInitialData()`  thunk action creator that was created in */src/actions/shared.js*.

It uses the thunk signature of `function xyz() { return dispatch => {...} }`.

Inside it invokes our Promise-based `getInitialData()` async request, then it dispatches the resulting data entities in order to fill our Redux store.

We should invoke this from App since this is the entry point to our application. Now in order to invoke this we need to expose the action as props by using ‘react-redux’ `connect` method. We do this in */src/components/App.js*.

