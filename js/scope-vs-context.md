## Scope v.s. Context
### Definition
- `Scope`用以紀錄當觸發函式時，函式中所使用的變數。每一次的觸發函式執行，`Scope`皆是獨立的。
- `Context`是一個擁有某一函式的`Object`，函式中`this`永遠指向此`Object`。

## Execution Context
### Definition
`Execution Context`為JavaScript Runtime執行到某個函式時，為此次函式執行創造的一個小環境，此環境將會插入JavaScript Runtime的`Stack`中，等待後續被執行。

`Execution Context`可分成兩種狀態：`Creation Phase`和`Execution Phase`

- `Creation Phase`：直譯器創造`variable/activation object`，由該層環境下所有的變數、函式宣告、參數所組成。接著初始化`Scope Chain`，`this`的值在最後才會定義完成。
- 接著是`Execution Phase`，程式碼將會被轉譯且執行。
