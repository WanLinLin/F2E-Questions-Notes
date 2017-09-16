## Position

position有四種屬性：

1. static
2. relative
3. fixed
4. absolute

使用position屬性的元素，須使用top, bottom, left, right屬性做調整。上述四種調整屬性只適用於使用position的元素上。

### 1. static

`position: static;`

一般頁面中的元素預設的position屬性會預設為static。static並無特殊效果，即依瀏覽器預設渲染排版。

### 2. relative

`position: relative;`

使用relative的元素使用top, bottom, left, right來相對於**元素預設定位**做排版。

### 3. fixed

`position: fixed;`

使用fixed的元素使用top, bottom, left, right來相對於**頁面顯示範圍（viewport）**做排版。因此當頁面滑動時，元素位置不會改變。

### 4. absolute

`position: absolute;`

使用absolute的元素使用top, bottom, left, right來相對於**最近一個有使用position屬性的父元素**做排版，且該父元素的position值只能是relative, fixed或是absolute。

若父元素皆無使用position屬性，則會相對於**頁面範圍（document）**做排版。

-

上述relative, fixed, absolute三種position方式可用top, bottom, left, right調整元素位置，若未使用某屬性如top調整，該屬性即依元素預設定位排版，

in HTML:

```HTML
<!-- in the body tag -->
<div class="a">
  <div class="b">
  </div>
</div>
```

in CSS:

```CSS
div.a {
  position: absolute;
  top: 20px;
}

div.b {
  position: fixed;
  left: 10px;
  /*
    div.b的top並沒有設定，因此div.b的top位置會預設為在div.a裡預設的位置，
    並不會直接讓他 top: 0;
  */
}
```

## Reference
- https://www.w3schools.com/css/css_positioning.asp