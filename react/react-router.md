# React Route

## Router

```js
render(
  <Router routes={routes} history={browserHistory} />
  , document.getElementById('app')
)
```

## Route

```html
<Route path="/" component={App}>
  <IndexRoute component={Home} />

  <Route path="/repos" component={Repos}>
    <Route path="/repos/:userName/:repoName" component={Repo} />
  </Route>
  <Route path="/about" component={About} />
</Route>
```

用Route指派遇到特定的url path時該render哪些component，指派完後再把整包Route塞到Router裡，Route和Component一樣有階層關係

history參數則是指定react-router用哪種方式操作url

## Link

```html
<Link to="/fancy" activeClassName="active" />
```

Link和一般網頁上的`<a href="...">`很類似，可以讓url變成特定的樣子
另外可以透過activeClassName和activeStyle來設定Link是active的樣式。

當url是Link的to所指定的url狀態時，該Link就是active的狀態

## url

url：Route的path和Link的to參數的值

url可以帶有參數：

```js
"/fancy/:groupId/:userId"
```

當使用url變數時，在對應的component就可以以props.params來存取這些變數

## Index Page

因為首頁的url通常都包含在子網站的url中：

首頁url：`/`
其餘子網頁url：`/about, /photos, ...`

因此不論在首頁的url或是子網頁的url時，首頁Link都會是Active的狀態，因此可以使用`<IndexRoute>和<IndexLink>`來設置首頁的Route和Link，就不會有首頁保持active的狀態發生

## browserHistory

可以用`browserHistory.push(path)`來把url改成特定的樣子

```
browserHistory.push(path)
```