# Redux Thunk

redux-thunk是一個redux的middleware，middleware可以讓你在action被dispatch後，到action進入reducer前這段時間做一些事，如log或是做非同步處理

redux-thunk讓action creator可以回傳一個函式而不是純action，通常react-thunk用來延遲dispach派發action，也可以用來讓action在指定狀態下才被派發。

redux-thunk拿取兩個參數：dispatch和(getState)，在thunk中即可做邏輯判斷或做非同步處理，最後在適當時機dispatch action

```js
const fetchUser = (id) => (dispatch) => {
  dispatch({
    type: 'FETCH_USER_REQUEST'
  })


  api.fetchUser(id).then(
    res => dispatch({
      type: 'FETCH_USER_SUCCESS',
      response: res
    }),
    // will catch errors from fetchUser and won't catch the errors in first func in then
    error => dispatch({
      type: 'FETCH_USER_ERROR',
      text: 'sorry'
    })
  )
}
```

## Reference
https://github.com/gaearon/redux-thunk/