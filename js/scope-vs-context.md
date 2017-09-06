## Something about Scope and Context
### Scope
- `Scope`用以紀錄當觸發函式時，函式中所使用的變數。每一次的觸發函式執行，Scope皆是獨立的。
- `Scope Chain`是指執行函式時，由該函式的scope為首一路往外層函式的scope連接的鏈。因此在該函式執行時，若需使用未在該函式scope中出現的的變數，便會透過scope chain一路往外層scope尋找是否有該變數存在。

### Context
- `Context`是一個擁有某一函式的Object，函式中this永遠指向此Object。

### Execution Context
`Execution Context`為JavaScript Runtime執行到某個函式時，為此次函式執行創造的一個小環境，此環境將會插入JavaScript Runtime的`Stack`中，等待後續被執行。

`Execution Context`可分成兩種狀態：`Creation Phase`和`Execution Phase`

- `Creation Phase`：直譯器創造`variable/activation object`，由該層環境下所有的變數、函式宣告、參數所組成。接著初始化`Scope Chain`，`this`的值在最後才會定義完成。
- 接著是`Execution Phase`，程式碼將會被轉譯且執行。

## Reference
http://ryanmorr.com/understanding-scope-and-context-in-javascript/