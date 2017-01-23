### Redux Basics

> Last Updated on 7th Jan 2017.

- Writing `createStore` function for redux.

``` javascript
const createStore = (reducer) => {
  let state;
  let listeners = [];

  const getState = () => state;
  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(listener => listener() );
  };
  const subscribe = (listener) => {
    listeners.push(listener);

    return () => {
      listeners = listeners.filter((l) => l!== listener);
    }
  };

  dispatch({});
  return {getState, dispatch, subscribe};
}
```

- Combining 2 or more reducers pattern.

``` javascript
// Combine Reducers Pattern
const todoApp = (state = {}, action) => {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.todos, action)
  };
}
```

- `combineReducers` implementation

``` javascript
const combineReducers = (reducers) => {
  return (state = {}, action) => {
    return Object.keys(reducers).reduce(
      (nextState, key) => {
        nextState[key] = reducers[key](state[key], action);
        return nextState;
      }
    , {});
  };
};
```
