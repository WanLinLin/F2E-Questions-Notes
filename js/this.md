##How "this" works in JavaScript?
###Global Context
```
// In browsers
console.log(this === window); // true
```
###Function Context
####simple call

1.在`strict mode`中，`this`的值在函示被呼叫時並未被設置，因此`this`預設指向`global object`

```
function f1() {
  return this;
}
// In a browser:
f1() === window;
```

2.在`strict mode`中，`this`的值則是取決於函示執行時的`context`，若函示並非以`method`或`property`的方式呼叫，`this`將預設為`undefined`

```
function f2() {
  'use strict'; // see strict mode
  return this;
}

f2() === undefined;
window.fw() === window; // true
```

###call() v.s. apply
可以使用`call()`、`apply()`來將特定的物件綁定在函式上，作為該函式中`this`所指的對象。其中的差異只有呼叫函式時傳入參數的傳法，call為一個一個船，apply為傳入一個參數陣列。

`call(contextObject, firstArg, secondArg,...)`
`apply(contextObject, [firstArg, secondArg,...])`

```
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

###bind()
`bind()`會將特定的物件綁定在該函式上，並回傳一個新的一樣的函式但`this`綁定在傳入的特定物件上。

需注意的是新回傳的函式將永遠綁定在該特定物件上，不能再用`bind()`再次綁定。

```
function f() {
  return this.a;
}

var g = f.bind({a: 'azerty'});
console.log(g()); // azerty

var h = g.bind({a: 'yoo'}); // bind only works once!
console.log(h()); // azerty
```

###Arrow Function
在arrow function被**創建**時，`this`會綁定在當前`Execution Context`的`this`所指向的物件上，且不會再被如`call() apply()`此類函示所改變。

###As a DOM event handler
當function作為event handler時，function中的this將指向該event handler所被綁定的DOM element上。