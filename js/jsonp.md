## JSONP

JSONP是一種利用HTML中`script`標籤不受CORS安全性限制的特性，以存取不同網域資源的方法。

### 範例

In HTML:

```HTML
<script src="jsonp.php">
```

In PHP:

```PHP
<?php
$myJSON = '{ "name":"Leo", "age":24, "city":"Miaoli" }';

echo "myFunc(".$myJSON.");";
?>
```

In JavaScript:

```JS
function myFunc(myObj) {
    document.getElementById("name").innerHTML = myObj.name;
}
```

需注意的是在PHP中必須將Response資料echo成JavaScript的語法回傳給client，因為在client端是利用script標籤讀取此PHP檔案，在server端執行完PHP程式碼後，最後還是會回到client端以JavaScript執行接收到的資料。

### 備註
- 在HTML中的script標籤src屬性可以指定帶有參數的url讓request更有變化
- 可以利用JavaScript動態新增JSONP讓存取資源變得更動態
- JSONP並沒有使用XMLHttpRequest或fetch的方式存取資源

### Resource
- https://www.w3schools.com/js/js_json_jsonp.asp