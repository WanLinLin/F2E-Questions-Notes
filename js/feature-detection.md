# Feature Detection v.s. Feature Inference v.s. UA String

## Feature Detection

寫段程式碼檢查程式碼運行的瀏覽器環境是否含有指定的規格。

若瀏覽器尚未實作出指定的規格，則可以選擇執行該瀏覽器可運行的較低品質但可接受的程式碼。

業界通常使用的標準函式庫：Modernizr

## Feature Inference

根據資料推斷程式碼運行的瀏覽器環境是否含有指定的規格，此作法僅以現有資料做推斷，並非長久之計。若未來瀏覽器環境實作出該功能或是有些瀏覽器環境並非如此簡單能夠直接推斷，將會造成錯誤結果。

### 範例
情境：假設已知Chrome實作了`Text`函式，也已知Chrome並沒有IE有實作的`applyElement`。

推斷：若瀏覽器環境沒有`applyElement`，則應該含有`Text`函式。

謬誤：某瀏覽器既沒有實作`applyElement`也沒有實作`Text`，推斷發生錯誤。

## UA String

UA String(User Agent String)，就是一串敘述某裝置及其搭載瀏覽器軟體的字串。

範例UA String：
> Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36

UA String同樣也可用來作為判斷程式碼運行環境是否含有某些規格的依據，此方式較Feature Inference更為精確。然而也因其太具針對性，規格判斷將過於瑣碎，或是當瀏覽器更新時將不再適用。

## Reference
- https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Feature_detection
- http://lucybain.com/blog/2014/feature-detection-vs-inference/