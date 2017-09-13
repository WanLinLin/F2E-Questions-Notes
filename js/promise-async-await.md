## promise

promise用於執行「耗時且不需要即時取得結果的程式碼」。以網頁開發為例，可以利用promise來非同步與後端取得資料，使其餘前端介面渲染程式碼繼續執行不會被block住。

promise的執行結果使用then與catch來做後續處理。

```JS
let comments = {
    "1": "nice",
    "2": "sharp",
    "3": "excellent"
};

function getComments() {
    return new Promise((resolve, reject) => {
            if (comments)
                setTimeout(() => resolve(comments), 1000);
            else
                setTimeout(() => reject("no comments"), 1000);
        }
    );
}
    
getComments()
    .then(comments => {
        comments[4] = "good job";
        return comments;
    })
    .then(comments => console.log(comments))
    .catch(err => console.log(err));
```

## async and await

async關鍵字置於含有promise的function前面，使其變成async function非同步函式，以避免過度阻礙後續程式碼執行。

await關鍵字只能再async function中使用，主要用於會return promise的expression前，等待promise執行完畢後，將其解析成值，若是promise被reject則會丟出error。

```JS
async function printComments() {
    try {
        let comments = await getComments();
        console.log(comments);
    }
    catch(err) {
        console.log(err);
    }
}

printComments();
console.log("I will be printed out before the comments");
```

async和await必須合併使用，缺少其中一個都無法達到預期的效果。然而async和await其實都是基於promise的語法，如上述的程式碼可使用純promise達到一樣的效果：

```JS
getComments()
    .then(comments => console.log(comments))
    .catch(err => console.log(err));

console.log("I will be printed out before the comments");
```