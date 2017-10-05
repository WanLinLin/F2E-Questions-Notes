# React Redux

一般而言，將component分為presentational和container以分別處理純呈現邏輯以及與資料相關的操作邏輯

## Presentational Component

- 目的：component要怎麼呈現在頁面上
- 要不要管redux：不用管redux
- 資料讀取：由props讀資料
- 改變資料：觸發props的callback
- 怎麼被寫的：手寫出來的

```js
let Number = ({ onNumberClick }) = {
  return (
    <span onClick={() => onNumberClick()}>
      {props.number}
    </span>
  )
}
```

## Container Component

- 目的：component要怎麼運作（資料怎麼抓，state怎麼更新）
- 要不要管redux：要管redux
- 資料讀取：由redux的state讀資料
- 改變資料：dispatch Redux actions
- 怎麼被寫的：通常是由React Redux的connect產生出來的

```js
// maps state to component props
const mapStateToProps = state => {
  return {
    number: state.number
  }
}

// adds dispatch functions to component props
const mapDispatchToProps = dispatch => {
  return {
    onNumberClick: () => {
      dispatch(add(1))
    }
  }
}

// connects mapping functions and presentatioal component to be a container component
Number = connect(
  mapStateToProps,
  mapDispatchToProps
)(Number)
```

### connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])

connect將presentational component加上自定義的mapStateToProps、mapDispatchToProp等函式轉換成container component

- 若不傳入mapStateToProps則預設此container不會因為state的更新而有動作
- 若不傳入mapDispatchToProps則預設注入dispatch到presentational component中以供存取

### mapStateToProps(state, ownProps): stateProps

mapStateToProps是一個函式，當state有更新時，此函式就會被呼叫。若是有給定第二個參數時，就會傳入component被給予的的props以供存取

此函式回傳一個object，此object將會被merge進component的props

### mapDispatchToProps(dispatch, ownProps): dispatchProps

mapDispatchToProps可以是一個object或是函式：

若是傳入物件，則物件中的每個函式都會被認定為redux action creater，並會將action creaters bind到dispatch上。只要在presentational component中使用這些用action creaters 做成的 dispatchProps，則這些action creaters就會立即被dispatch

```js
const actionCreater = {
  addTodo: (text) => ({
    type: 'ADD_TODO',
    text: 'hey'
  })
}

Number = connect(null, actionCreater)(Number)
```

若是傳入函式，則此函式將有dispatch可以使用，並回傳一個含有callbacks的object

## Provider

在使用react-redux的connect之前，必須將其parent component使用Provider包起來，Provider會讓所有child component中的connect可以使用store

```html
<Provider store={store}>
  <Root />
</Provider>
```

- http://redux.js.org/docs/basics/