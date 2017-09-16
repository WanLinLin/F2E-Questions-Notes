# display

## block-level v.s. inline

HTML元素中主要分為兩大類：block-level及inline兩種類型的元素，他們具有不同的排版特性

### block-level元素

特性：block-level的元素會佔據新的一行的空間，填滿該行最左到最右可及範圍，且可指定寬、高

以下是一些block-level元素：

```HTML
<div>
<h1> - <h6>
<p>
<form>
<header>
<footer>
<section>
...
```

[更詳細的block-level元素列表](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Block-level_elements)

### inline元素

特性：inline的元素不會佔據新的一行的空間，只會使用它需要使用的空間

以下是一些inline元素：

```HTML
<span>
<a>
<img>
...
```

[更詳細的inline元素列表](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)

## the value of display

使用display屬性可以更改HTML元素預設的排版特性，如把inline排版特性的span元素改成block元素排版方式，使其從佔有最少須用空間變成佔有一整行的區塊並可指定寬高等。

### block

`display: block;`

讓元素變成block排版元素排版方式

### inline

`display: inline;`

讓元素變成inline排版元素排版方式

### inline-block

`display: inline-block;`

當元素被設定為inline-block時，其排版方式與inline相同，但該元素可以被指定width和height。

### none

`display: none;`

被設定為none的元素在頁面中不會被顯示，也不會佔據空間。與其相似的屬性有`visibility: hidden;`，其使元素不被顯示，但會佔據頁面上的空間。

[更詳細的display值列表](https://www.w3schools.com/cssref/pr_class_display.asp)

## Reference
- https://www.w3schools.com/css/css_display_visibility.asp
- https://developer.mozilla.org/zh-TW/docs/Web/HTML/Block-level_elements
- https://www.w3schools.com/cssref/pr_class_display.asp
- https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements