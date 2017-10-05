# async actions

當觸發一個非同步API時，通常會有兩個關鍵時刻：

- 當你觸發的那一刻
- 當API被解決的那一刻

上述兩種事件通常都需要更新app的state，通常會有下列三種action

- 通知reducer已經觸發api了
- 通知reducer api已經被解決了
- 通知reducer api失敗了

actions可能會像是：

```js
{ type: 'FETCH_POSTS_REQUEST' }
{ type: 'FETCH_POSTS_FAILURE', error: 'Oops' }
{ type: 'FETCH_POSTS_SUCCESS', response: { ... } }
```


# Reference
- http://redux.js.org/docs/advanced/AsyncActions.html