# Component

是一個會產生react element的函式

- 大寫字首
- 必須只回傳一個元素，若要回傳很多元素必須用一個元素包起來再回傳
- 針對props來說，必須是pure function

## Functional Components

純function，將props作為參數，並回傳要被render的東西。

## Class Components

用JavaScript ES6 class語法寫的component，一定會有render函式來回傳react element。

class components還有控制生命週期的`componentDidMount`和`componentWillUnmount`兩個函式。


# Key
當要render一個list的時候，必須指定key給元素們，例如：

```js
const books = [
  {id: 1, title: 'apple'},
  {id: 2, title: 'bagle'}
]

function BookList(props) {
  const elements = books.map(
    book => <li key={book.id}>{book.title}</li>
  )

  return (
    <ul>{elements}</ul>
  )
}
```

key讓react知道何時該新創、摧毀一個component。
比如說一個list裡面有新的key出現，react就會新創一個component
如果一個list裡面有舊的key被刪除，react就會把這個component刪除


# Escape

當HTML中有出現特殊字符如`< " > &`等等字元時，可能會讓瀏覽器呈現出非預想結果的頁面。因此會escape這些特殊字元，將這些字元轉換成如`&quot;`這種字串後再傳給瀏覽器，如此可以防止惡意攻擊或其他意外的發生。

# State

## State updates may be asynchronous
React因效能考量有可能會將數次的`setState()`整合在一批再一次update，因此不應將state或props的值作為運算下一個state的值的參數。

```js
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

然而，setState除了可以接受物件參數外，也可以接受函式作為參數

```js
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

如此便可解決state非同步更新的問題

# tips

- 在JavaScript中，`true && expression`將會回傳`expression`，而`false && expression`將會回傳`false`

# References
- https://facebook.github.io/react/tutorial/tutorial.html
- https://facebook.github.io/react/docs/hello-world.html