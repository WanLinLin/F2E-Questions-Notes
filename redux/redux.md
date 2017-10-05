# Why Redux

因程式在執行時，mutation及asynchronicity是人類最難以光靠想像就知道state的改變是因為什麼事情的發生，因此會很難除蟲

# Core Concepts

將action(js object)傳入reducer(js function)去修改state，如此在發現state改變時，可以由action來知道為什麼他改變了

# Three Principles

- single source of truth: 整個app的state只用一個object來紀錄，並存在store中

- state is read-only: 只能透過發動action才能改變state

- changes are made with pure functions: 用pure reducers(functions)來回傳一個新的改變後的state

# Basic Components

## action

an `object` describing the action to the state

```js
const action = {
  type: 'ADD',
  number: 4
}
```

## action creater

a `function` produces an action

```js
function add(number) {
  return {
    type: 'ADD',
    number
  }
}
```

## reducer

a `pure function` reads the action and make a new modified state

```js
function reducer(prevState, action) {
  switch(action.type) {
    case 'ADD':
      return Object.assign({}, prevState, action.number)
    default:
      return prevState
  }
}
```

## store

store links state, action and reducer all together

```js

// attach the reducer on a state within store
let store = createStore(reducer)

// access state
store.getState()

// update the state
store.dispach(add(2))

// add a listener
store.subscribe(listener)
```

# Reference

all contents in the basic guide

- http://redux.js.org/docs/basics/