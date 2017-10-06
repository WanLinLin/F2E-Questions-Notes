# Immutable.js

## Features

### 1. Immutable Collection是value不是object

不要把Immutable Collection看成是js object，要把他看成是value

因為object可以被改變，而Collection並無法被改變，而是一個又一個新的改變後的object(也不是完全不一樣，因immutable有特殊實做細節)

### 2. Immutable Collection無法被改變

若要更改Collection，immutable將會回傳一個新的改變後的值，原本的變數並不會被改變

```js
const { Map } = require('immutable')

const map1 = Map({ a: 1, b: 2, c: 3})
const map2 = map1.set('b', 50)

map1.get('b') + " vs. " + map2.get('b') // 2 vs. 50
```

### 3. 使用`Immutable.is()`或是`.equals()`來比對兩個變數

不要使用`===`比較兩個Immutable Collection的相等性，因為`===`對於js object比的是變數的reference

在Immutable中除了clone外，所有被改變後的變數都是一個新的object，所以必須使用純比較object的值的方式比較兩個Immutable Collection

```js
const map1 = Map({ a: 1, b: 2, c: 3})
const map2 = Map({ a: 1, b: 2, c: 3})

console.log(map1.equals(map2)) // true
console.log(Immutable.is(map1, map2)) // true
```

### 4. 複製Immutable Collection

因為Immutable Collection不會被改變，因此要複製一個Immutable Collection，只要製造一個新的變數並指向這個collection

```js
const map1 = Map({ a: 1, b: 2, c: 3})
const clone = map1
```

### 5. 和JS原生物件相似

- Immutable.List ==> Array
- Immutable.Map ==> Map
- Immutable.Set ==> Set

Immutable Collection通常都可以使用對應於JS原生物件的method

### 6. Immutable可以接受JS原生物件以創造Collection

使用JS原生物件創造Immutable Collection可讓JS原生物件使用更多Immutable所提供的API，並在最後使用`toObject()`傳回原本的JS物件

如果使用JS原生物件創造Immutable的Map，則Key永遠為String型態

```js
const { fromJS } = require('immutable')

// 一般的JS物件存取，會先將key轉換成string型態
const obj = { 1: "one" }
Object.keys(obj) // [ "1" ]
assert.equal(obj["1"], obj[1])   // "one" === "one"

// 由於Immutable Map的Key可以是任何JS型態，因此Immutable
// 不會先幫你轉成String，因此當使用JS物件轉換成Immutable Map
// 要把key值以string的方式輸入才可以存取
const map = fromJS(obj)
assert.notEqual(map.get("1"), map.get(1)) // "one" !== undefined
```

### 7. Lazy Seq

Seq讓Collection的操作變得必要時才會執行，任何Immutable Collection被`toSeq()`轉換成Seq

```js
const { Seq } = require('immutable')

// oddSquares的filter跟map並不會真的被執行，因為oddSquares的值並沒有被使用到
const oddSquares = Seq([ 1, 2, 3, 4, 5, 6, 7, 8 ])
  .filter(x => x % 2)
  .map(x => x * x)
```

### 8. Batching Mutations

在使用Immutable Collection時，若要在return最終值之前對該collection使用一般的collection methods做一系列的操作，會導致效能下降

Immutable提供了`withMutations()`，讓你可以在callback參數中做一系列的mutation，而不會造成上述的效能問題

```js
const { List } = require('immutable')
const list1 = List([ 1, 2, 3 ]);
const list2 = list1.withMutations(function (list) {
  list.push(4).push(5).push(6);
});
assert.equal(list1.size, 3);
assert.equal(list2.size, 6);
```

## Some Methods

- fromJS()
>Deeply converts plain JS objects and arrays to Immutable Maps and Lists.

- toArray(), toObject()
>Collections can be converted to plain JavaScript Arrays and Objects shallowly

- toJS()
>convert Collections to plain JavaScript Arrays and Objects deeply

- mergeDeep(nestedObject)
>把兩個部份相符的object深度融合

- getIn(pathNodes)
>依照給定的路徑節點回傳該值

- updateIn(pathNodes, callback)
>依照給定的路徑節點更新該值

```js
// expamples
const { fromJS } = require('immutable')
const nested = fromJS({ a: { b: { c: [ 3, 4, 5 ] } } })

const nested2 = nested.mergeDeep({ a: { b: { d: 6 } } })
// Map { a: Map { b: Map { c: List [ 3, 4, 5 ], d: 6 } } }

console.log(nested2.getIn([ 'a', 'b', 'd' ])) // 6

const nested3 = nested2.updateIn([ 'a', 'b', 'd' ], value => value + 1)
console.log(nested3);
// Map { a: Map { b: Map { c: List [ 3, 4, 5 ], d: 7 } } }

const nested4 = nested3.updateIn([ 'a', 'b', 'c' ], list => list.push(6))
// Map { a: Map { b: Map { c: List [ 3, 4, 5, 6 ], d: 7 } } }
```

## Reference
https://facebook.github.io/immutable-js/