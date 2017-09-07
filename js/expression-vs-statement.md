## Expression v.s. Statement

### expression
`expression`產生「值」，在任何需要填入「值」的地方皆可以填入`expression`

```JS
myvar
3 + x
```

### statement

`statement`產生「動作」，如`loop`、`if`等等程式碼。在JavaScript中，可填入statement的地方也可以填入expression，此時的statement稱為`expression statement`。

反之並不成立，無法在任何可以填入expression的地方填入statement，如不可在function call的參數區域填入statement。

### function expression
function expression是一種值，可將其指派給變數。

#### anonymous function expression

```JS
function() {}

// normal usage
var f = function() {};
```

#### named function expression

```JS
function foo() {}

// normal usage
var f = function foo() {};
```

此function expression的名稱foo，只適用於該函數中。如在函式中需使用遞迴時可以使用foo()呼叫此函數。

然而，named function expression難以與function declaration區分，他們有不同的效果。

function expression產生值（此函數），而function declaration產生動作：創造一變數，並將函數值指派給他，且只有function expression可以被immediately invoked，function declaration無法。

在JavaScript中，()裡的程式碼會被當作expression解析（expression context）
，因此Immediately Invoked Function Expression才會看起來是這樣：

```JS
(function() {
  // do something
})();

// or

(function() {
  // do something
}())
```

## Reference
http://2ality.com/2012/09/expressions-vs-statements.html