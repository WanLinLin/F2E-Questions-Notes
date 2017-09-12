# Closure

## Definition

`Closure`是一個function與其lexical environment的組合。

`lexical environment`是一個function可以使用該function父環境（parent scope）的變數、函式的這種環境。

## Usage

### Data hiding and Encapsulation

```JS
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var counter1 = makeCounter();
var counter2 = makeCounter();

alert(counter1.value()); /* Alerts 0 */
counter1.increment();
counter1.increment();
alert(counter1.value()); /* Alerts 2 */
alert(counter2.value()); /* Alerts 0 */
```

## specials
在一個function中製造出的closures會**共用同一個lexical environment**。

### example code

HTML:

```HTML
<p id="help">Helpful notes will appear here</p>
<p>E-mail: <input type="text" id="email" name="email"></p>
<p>Name: <input type="text" id="name" name="name"></p>
<p>Age: <input type="text" id="age" name="age"></p>
```

JavaScript:

```JS
function showHelp(help) {
  document.getElementById('help').innerHTML = help;
}

function setup() {
  var helpText = [
    {'id': 'email', 'help': 'Your e-mail address'},
    {'id': 'name', 'help': 'Your full name'},
    {'id': 'age', 'help': 'Your age (you must be over 16)'}
  ];
    
  // 用for迴圈製造出了3個closures給不同的element event使用，
  for (var i = 0; i < data.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function() {
      showHelp(item.help);
    }
  }
}

setup();
```

因var變數是function scope，因此三個closure callbacke會共用同一個item變數，在p標籤onfocus被觸發時執行callback，此時callback呼叫showHelp時，參數item.help已經被loop到helpText的最後一個元素了，因此不管點哪個p標籤，都會顯示age的訊息。

在ES6的let keyword出現之前的解法可以參考reference中mozilla頁面的教學使用function factory或是IIFE(Immediately Invoked Function Expression)的方式解決。但有了let的出現，其實只要把for裡面的item變數改用let宣告就可以解決問題了，因為let是block scope。（mozilla教學頁面也有提到）

然而因為let的出現，應能有效減少此類程式碼會出現的誤解。

## Reference
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
- https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36