# Webpack

webpack是一個模組組合器（module bundler），原致力於將網站模組化開發流程整合，然而因為webpack社群努力，現在webpack中也可以使用事物處理器（task runner）的功能了，如：

- 清除build目錄內容物
- 發佈產品
- 醜化檔案
- ...等等功能

而webpack的主要功能就是將js、css這種互相link的檔案在最後要運行網頁的時候一次打包成一個或多個檔案並讓html引入

webpack會依據config file的設定，從entry開始藉由各種檔案的loader幫忙，掃出dependency graph，最後整合產出在設定的output資料夾中。

## config file

- entry：開始掃檔案的地方
- module：設定各式loader
- resolve：設定除了node_modules之外特定的掃描原則，如某些副檔名或哪些資料夾
- output：設定產出檔案的檔名、路徑
- plugins: 讓webpack做一些除了bundle之外的事，如uglify

`webpack.config.js`和`webpackfile.js`是webpack預設的設定檔名，若要使用自定義的設定檔名，使用`--config`來設定參數

---

## Features

### hot module replacement

開發時若檔案有更改，HMR讓瀏覽器的頁面直接重新整理，不必重新執行webpack。然而HMR與LiveReload或BrowserSync不同的地方是，在react開發中，他可以維持state的狀態並更新需要更新的部份，不會讓整個頁面重新整理而讓state產生變動。

>enhance development experience by updating code in the browser without a full refresh

### code splitting

除了可分包產生不同的小bundles外，還有lazy loading讓網頁需要時才讀取檔案

### asset hashing

可以在檔名中加上hash，如`app.as23ak4h5.js`讓client知道檔案已經產生變動，需要重新下載新版的檔案

## References
- https://survivejs.com/webpack/what-is-webpack/