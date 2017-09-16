# Functional Programming

## Core Concepts

### pure functions

- 可以完全看作是數學的函數，若輸入同樣的input，總是輸出同樣的output
- 可以將直接將程式碼中任何寫function call的地方直接取代成其輸出值而不會有錯誤

```
const double = x => 2 * x;

const a = double(2);
// the line above can simply replace by the line below
// because pure functions take the same input always
// return the same value, we can see the function call as a value
const a = 4;
```

- 不會產生side effect，如不會改變函式外部的值、不會印出東西
- 不依賴外部會變動的state，完全獨立於外部的state

優點：

1. 非常容易重複使用
2. 因外部狀態產生的bug可以完全忽略是pure function引起的
3. 因其獨立性，適合應用於平行運算處理、分散式系統
4. 因其獨立性，可以輕易的重組於程式碼中，提高程式碼的彈性及隨時準備應對未來的改變

### function composition

將多個function當作輸入值，並回傳一個會做完所有傳入function的function。

以下pipe就做了function composition：

```
const toSlug = pipe(
  split(' '),
  map(toLowerCase),
  join('-'),
  encodeURIComponent
);

console.log(toSlug('JS Cheerleader')); // 'js-cheerleader'
```

### avoid shared state, mutating state

### avoid side effect

- Modifying any external variable or object property
- Logging to the console
- Writing to the screen
- Writing to a file
- Writing to the network
- Triggering any external process
- Calling any other functions with side-effects

最主要就是要避免race condition造成的悲劇

## Reference
- https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0
- https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0