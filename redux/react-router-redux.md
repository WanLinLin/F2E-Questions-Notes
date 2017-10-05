# react-router-redux

在state中新增一個routing，value會跟瀏覽器的url同步

## Setup

### Step1:
在redux createStore的時候把routerReducer也一起塞進去

```js
import { routerReducer } from 'react-router-redux'

// Add the reducer to your store on the `routing` key
const store = createStore(
  combineReducers({
    ...reducers,
    routing: routerReducer
  })
)
```

### Step2:
讓react-router-redux可以存取history(url)跟store(dispatch)

```js
// Create an enhanced history that syncs navigation events with the store
const history = syncHistoryWithStore(browserHistory, store)
```

設置完畢！

## Usages

1. 想要listen url變更的event

```js
const history = syncHistoryWithStore(browserHistory, store)

history.listen(location => analyticsService.track(location.pathname))
```

2. 在container component存取router state(react-router提供的功能)

```js
function mapStateToProps(state, ownProps) {
  return {
    id: ownProps.params.id,
    filter: ownProps.location.query.filter
  };
}
```

3. 透過dispatch action來改變routing

```js
import { createStore, applyMiddleware, combineReducers } from 'redux'
import { browserHistory } from 'react-router'
import { routerMiddleware, push } from 'react-router-redux'
import reducers from './reducers'

const reducers = combineReducers({
  ...reducers,
  routing: routerReducer
})

// 讓react-router-redux的middleware在action進到reducer
// 改變state.routing前，先改變瀏覽器的url
const middleware = routerMiddleware(browserHistory)
const store = createStore(
  reducers,
  applyMiddleware(middleware)
)

// Dispatch from anywhere like normal.
store.dispatch(push('/foo'))
```

## Middleware Action Creators

- push(location)
- replace(location)
- go(number)
- goBack()
- goForward()

## Reference
https://github.com/reactjs/react-router-redux