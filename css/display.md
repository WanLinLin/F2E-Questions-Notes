## Display

每個元素都會有預設的display值，最主要有block及inline這兩種屬性

以下列出幾個基本的值：

### block

`display: block;`

被設定為block的元素會佔據新的一行的空間，填滿該行最左到最右可及範圍

以下是預設為block的元素範例：

```HTML
<div>
<h1> - <h6>
<p>
<form>
<header>
<footer>
<section>
```

### inline

`display: inline;`

被設定為inline的元素不會佔據新的一行的空間，只會使用它需要使用的空間

以下是預設為inline的元素範例：

```HTML
<span>
<a>
<img>
```

### none

`display: none;`

被設定為none的元素在頁面中不會被顯示，也不會佔據空間。與其相似的屬性有`visibility: hidden;`，其使元素不被顯示，但會佔據頁面上的空間。

### inline-block

`display: inline-block;`

當元素被設定為inline-block時，其排版方式與inline相同，但該元素可以被指定width和height。

## Reference
- https://www.w3schools.com/css/css_display_visibility.asp