# plugins

## extract-text-webpack-plugin

將js檔案中引用的css檔案取出產成css檔案，而不是inline在bundled js裡面

## assets-webpack-plugin

>emits a json file with assets paths

### why is this useful?

>When working with Webpack you might want to generate your bundles with a generated hash in them (for cache busting). This plug-in outputs a json file with the paths of the generated assets so you can find them from somewhere else.

## HashedModuleIdsPlugin

>cause hashes to be based on the relative path of the module, generating a four character string as the module id. Suggested for use in production.