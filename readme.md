# Description

This repo aims to reproduce a strange bug in the way webpack calculates its total runtime.

# Steps

First install dependencies using `npm install`.

Try running a webpack build directly with a command like `./node_modules/webpack/bin/webpack.js`. You should see a time displayed of around a second or less.

```
Hash: c5cf6ea714d9a7bbb009
Version: webpack 4.9.1
Time: 370ms
Built at: 2018-05-28 22:19:43
  Asset       Size  Chunks             Chunk Names
main.js  545 bytes       0  [emitted]  main
Entrypoint main = main.js
[0] ./index.js 0 bytes {0} [built]
```

Now if you run webpack via `webpack-serve` with a command like `./node_modules/webpack-serve/cli.js`, the time calculation shown by webpack is wrong, it has around 10 seconds added to it, even though there is barely any extra processing going on, and it clearly still takes less than a second to complete.

```
ℹ ｢hot｣: webpack: Compiling...
ℹ ｢hot｣: WebSocket Server Listening at localhost:8081
ℹ ｢serve｣: Project is running at http://localhost:8080
ℹ ｢serve｣: Server URI copied to clipboard
ℹ ｢hot｣: webpack: Compiling Done
⚠ ｢wdm｣: Hash: 4651e8a7af883547a70f
Version: webpack 4.9.1
Time: 12438ms
Built at: 2018-05-28 22:22:22
  Asset      Size  Chunks             Chunk Names
main.js  78.1 KiB       0  [emitted]  main
Entrypoint main = main.js
 [0] (webpack)-hot-client/client/log.js 2.4 KiB {0} [built]
 [1] ./index.js 0 bytes {0} [built]
 [3] ./node_modules/querystring-es3/decode.js 2.45 KiB {0} [built]
 [4] ./node_modules/querystring-es3/index.js 127 bytes {0} [built]
 [5] ./node_modules/url/util.js 314 bytes {0} [built]
 [6] (webpack)/buildin/global.js 509 bytes {0} [built]
 [7] (webpack)/buildin/module.js 519 bytes {0} [built]
 [8] ./node_modules/node-libs-browser/node_modules/punycode/punycode.js 14.3 KiB {0} [built]
 [9] ./node_modules/url/url.js 22.8 KiB {0} [built]
[10] (webpack)-hot-client/client/socket.js 1.39 KiB {0} [built]
[11] (webpack)-hot-client/client/hot.js 4.91 KiB {0} [built]
[12] ./node_modules/loglevelnext/dist/loglevelnext.js 55.9 KiB {0} [built]
[13] (webpack)-hot-client/client?0518f298-c4f9-4814-93dd-afd5638f136d 2.47 KiB {0} [built]
[14] multi webpack-hot-client/client?0518f298-c4f9-4814-93dd-afd5638f136d ./index.js 40 bytes {0} [built]
[15] multi ./index.js 28 bytes {0} [built]
```

