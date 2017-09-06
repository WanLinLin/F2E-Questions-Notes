## How "this" works in JavaScript?

### Global Context
this指向global object

```JS
// In browsers
console.log(this === window); // true
```

### Function Context
#### simple call
函式被呼叫時並非以method或property的方式呼叫

1.直接呼叫f1函式，`this`預設指向`global object`

```JS
function f1() {
  return this;
}

// In a browser:
f1() === window; // true
```

2.在`strict mode`中，直接呼叫f2函式，`this`預設值為`undefined`。在global scope中所定義的函式f2屬於global object(window)的method，因此若是以`window.f2()`的方式呼叫f2函式，則this照常理就會指向呼叫他的object。

```JS
function f2() {
  'use strict'; // see strict mode
  return this;
}

f2() === undefined; // true
window.f2() === window; // ture
```

### call() v.s. apply()
可以使用`call()`、`apply()`來將特定的物件綁定在函式上，作為該函式中`this`所指的對象。其中的差異只有呼叫函式時傳入參數的傳法，call接受一連串的參數，apply則接受一個參數陣列。

`call(thisArg, firstArg, secondArg,...)`
`apply(thisArg, [firstArg, secondArg,...])`

```JS
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```

### bind()
`bind()`會將特定的物件綁定在該函式上，並回傳一個全新且一樣的函式但`this`綁定在傳入的特定物件上。

需注意的是新回傳的函式將永遠綁定在該特定物件上，不能再用`bind()`再次綁定。

```JS
function f() {
  return this.a;
}

var g = f.bind({a: 'abc'});
console.log(g()); // abc

var h = g.bind({a: 'def'}); // bind only works once!
console.log(h()); // abc

//but you can do like this
var h = f.bind({a: 'def'}); // use the original function to bind
console.log(h()); // def
```

### Arrow Function
在arrow function被**"創建"**時，this會指向當前Execution Context的this所指向的物件上，也就是arrow function中的this完全等於外面一層scope的this的值。且arrow function中的this的值在創建時被綁定就不會再被改變，如`call(), apply()`此類函示無法產生作用。

```JS
var obj = {
  bar: function() {
    var x = (() => this);
    return x;
  }
};

// 以obj的method方式執行bar函式，此時bar的execution context中的this應該指向obj，
// 因此x函式的this就會指向obj，並回傳此x函式給fn。
var fn = obj.bar();
console.log(fn() === obj); // true

// 將fn2的值設定為obj的bar函式，在執行fn2的函式時（第一個空括號），
// 此時的execution context的this並非以method或property的方式互叫，
// 因此this預設指向global object，此時x函式的this即為global object，
// 並回傳此函式。接著以第二個空括號執行此回傳的函式，就會得到global object的值。
var fn2 = obj.bar;
console.log(fn2()() == window); // true
```

### As a DOM event handler
當function作為event handler時，function中的this將指向該event handler所被綁定的DOM element上。

```
function q(e) {
  console.log(this);
}

var el = document.getElementById('As_a_DOM_event_handler')
el.addEventListener('click', q, false)

// when click the element, console shows:
// <h3 id="As_a_DOM_event_handler">As a DOM event handler</h3>
```


## Reference
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
