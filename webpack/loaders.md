# loaders

在webpack設定檔中的loaders使用的順序是由右至左、由下到上，但可以使用enforce設定來強至最先執行或最後執行

## style-loader

>adds CSS to the DOM by injecting a `<style>` tag

## css-loader

>the `css-loader` interprets `@import` and `url()` like `import/require()` and will resolve them

## postcss-loader

>postcss-loader is a tool for transforming CSS with JavaScript, is the equivalent of Babel for styling

## extract-text-webpack-plugin

>It moves all the required *.css modules in entry chunks into a separate CSS file. So your styles are no longer inlined into the JS bundle, but in a separate CSS file (styles.css).

## file-loader

>you can generate file names that are "content hashed" This helps a lot in making sure that clients don't accidentally use older versions of the file due to browser or CDN caches.

## image-loader

>minify png, jpeg, gif, svg images with "imagemin"