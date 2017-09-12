## Event Passing

大部分的event在DOM裡面的傳遞分成三個階段：

1. capture phase
2. target phase
3. bubbling phase

當按下某個元素時，event將會從最頂層父元素一路傳到你觸發的元素，再從該元素一路將event傳回最頂層父元素。

下圖清楚地描述了event傳遞的三個階段：

<img
    src="https://www.w3.org/TR/DOM-Level-3-Events/images/eventflow.svg"
    alt="event passing"
    style="width: 450px; border: solid; border-width: 1px"/>

### 範例

In HTML:

```HTML
<form>FORM
  <div>DIV
    <p>P</p>
  </div>
</form>
```

In JavaScript:

```JS
for(let elem of document.querySelectorAll('*')) {
    elem.addEventListener(
        "click",
        e => alert(`Bubbling: ${elem.tagName}`)
    );
}
```

按下P標籤結果的alert順序將會是：P > DIV > FORM > BODY > HTML，只能觀察到event bubbling的現象。

在一般使用情況下，並不會接觸到capture phase，若想接觸capture phase，必須在addEventListener第三個optional參數設為true。

In JavaScript:

```JS
for(let elem of document.querySelectorAll('*')) {
    elem.addEventListener(
        "click", e => alert(`Capturing: ${elem.tagName}`), true);
    elem.addEventListener(
        "click", e => alert(`Bubbling: ${elem.tagName}`));
}
```

按下P標籤結果的alert順序將會是：HTML > BODY > FORM > DIV > P > P > DIV > FORM > BODY > HTML。

### 備註
1. `event.currentTarget`指的是在event傳遞過程中，event正傳遞到的元素，值等同於handler中所使用的this。而`event.target`則永遠是你觸發的元素。

2. 可以利用`event.stopPropagation()`來停止event bubbling將event傳下去，然而若無周全的考量建議不要使用。如有些網頁中需要執行一些分析使用者行為的程式碼，若讓event停止往父元素傳，可能會讓分析程式碼無法準確抓到所有的使用者行為。


### Reference
- https://javascript.info/bubbling-and-capturing
- https://www.w3.org/TR/DOM-Level-3-Events/