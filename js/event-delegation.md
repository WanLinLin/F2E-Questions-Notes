##Event Delegation
###使用時機
當有多個元素且需使用EventListener處理event，且元素會動態新增刪除時
###目的
解決需在每個元素上新增EventListener的麻煩
###解法
將EventListener加在父元素上，利用event bubbling的特性，只需在bubbling階段父元素接收到event時，利用e.target找出是trigger了哪個子元素，進而做處理。
###Example Code
HTML

```
<ul id="parent-list">
	<li id="1">Item 1</li>
	<li id="2">Item 2</li>
	<li id="3">Item 3</li>
	<li id="4">Item 4</li>
	<li id="5">Item 5</li>
	<li id="6">Item 6</li>
</ul>
```

JS

```
document.getElementById("parent-list").addEventListener("click", function(e) {
	if(e.target && e.target.nodeName == "LI") {
		// List item found!  Output the ID!
		console.log("List item ", e.target.id, " was clicked!");
	}
});
```