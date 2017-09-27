## --watch and webpack-dev-server

- 使用`webpack --watch`來讓webpack監控你的程式碼，並自動重新build

- 使用`webpack-dev-server`來讓webpack提供開發用伺服器，將build出的檔案放置在記憶體中並運行一server供存取網頁。WDS也提供了HMR(Hot Module Replacement)的功能，在WDS rebuild的時候不會重整整個頁面讓state被重置，會保留住state，讓react開發更有彈性。

- 因更改config file不會重跑webpack，所以要用nodemon監控config file，在更改config file後，自動重新執行webpack


- 除了自動更新及HMR外，webpack-dev-server也可以使用middleware的方式整合進node server，也可以設定proxy參數與其他伺服器溝通