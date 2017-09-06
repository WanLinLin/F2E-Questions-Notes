##Undeclared, Undefined and Null

###undeclared

如果一個變數並非以var關鍵字宣告，則此變數則為**undeclared**。無論此變數在何處宣告（Global/Function Scope），此變數將會存在於Global Scope中。

```
var declaredVariable = 1;

function scoppedVariables() {
  undeclaredVariable = 1;
  var declaredVariable = 2;
}

scoppedVariables();

undeclaredVariable; // 1
declaredVariable; // 1
```

然而，若是處於`strict mode`中，則以undeclared方式宣告的變數則會產生錯誤，無法使用。

###undefined

- 若一變數使用var宣告但並未被初始化，則此變數為undefined

```
var undefinedVariable; // undefined
typeof undefinedVariable; // "undefined"
```

- 若呼叫一尚未宣告的**函式**或**變數**，則直譯器則會出現`not defined`錯誤

#####檢視變數是否為undefined
```
if (typeof(variable) !== "undefined") {
  console.log('variable is not undefined');
}
```

###null

- 變數需特別指定為`null`才會成為null變數
- 使用typeof檢視null變數時，回傳為object
- null通常用來作為function的回傳值

```
var nullVariable = null; // null
typeof nullVariable // "object"
```

#####檢視變數是否為null
```
if( variable === null ) {
  console.log('variable is null');
}
```