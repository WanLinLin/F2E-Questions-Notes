# float and clear

## float

float屬性的出現是為了讓網頁內容產生**文繞圖**的效果而出現

因此，float屬性讓該元素脫離其原本網頁排列方式，浮在頁面上面一層，並往指定方向靠齊。對於網頁上其餘元素來說，依元素是block-level或inline會有不同的影響：

### 對於block-level元素來說：

因block元素主要作為**網頁區塊分割**，因此block-level元素會無視於float元素而按照其原本排列方式排版（因float元素浮在網頁上），然而在block-level元素裡的文字會對於float元素產生文繞圖的效果

範例：[去JSFiddle看效果](https://jsfiddle.net/ftm5sLst/)

### 對於inline元素來說：

因inline元素主要就是用於**網頁文字**內容，而float則是讓元素產生文繞圖效果，因此inline元素會直接對於float元素產生文繞圖的效果，不會有像block-level元素出現在float元素底下的排版情形產生

範例：[去JSFiddle看效果](https://jsfiddle.net/ftm5sLst/2/)

## clear

clear屬性套用在元素上會使該元素指定方向上不能有float元素的存在，且clear屬性只對**block-level元素**起作用

範例：[去JSFiddle看效果](https://jsfiddle.net/ftm5sLst/3/)

## Reference
- https://www.w3schools.com/css/css_float.asp
- https://www.w3schools.com/cssref/pr_class_float.asp
- https://www.w3schools.com/cssref/pr_class_clear.asp
- http://carlos-studio.com/2013/08/06/css-float%E5%B1%AC%E6%80%A7%E8%88%87clear%E5%B1%AC%E6%80%A7/
- https://stackoverflow.com/questions/30748237/css-clear-on-inline-elements