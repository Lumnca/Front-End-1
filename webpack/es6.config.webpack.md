#### [webpack 配置用于Es6 语法的例子](#top) <b id="top"></b>
`需求添加 rollup 用于代码合并,添加bable 用于代码转换,注意:一切都安装在本地 而不是全局安装 `

------

- [x] [`1.安装webpack 环境命令`](#target1)
- [x] [`2.devtool`](#target2)
- [x] [`3.在package.json 里面增加script 命令用于打包`](#target3)
- [x] [`4.此时`](#target4)

------

#####  [1.安装webpack 环境命令](#top) <b id="target1"></b> 
```node
cnpm init

cnpm install -D webpack webpack-cli 
cnpm install rollup -D

```

`rollup.config.js 配置信息`

```node
export default {
    input: './src/index.js',
    output: {
      file: './src/rollupjs/index.min.js',
      format: 'iife'
    }
  }
```

```npm 
cnpm install babel babel-loader babel-core babel-preset-env 

/* babel-loader@8 requires Babel 7.x (the package '@babel/core') */
npm install -D babel-loader@7.1.5
```
`webpack.config.js配置文件`

```node
const path = require('path');

module.exports = {
    devtool:"source-map", //正常打包请换为: eval
    entry: {
        index: './src/index.js'
    },
    mode: 'development', //mode: 'production',
    output: {
        filename: '[name].min.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [{
            test: /\.js$/,
            exclude: /(node_modules)/,
            use: {
                loader: 'babel-loader',
                options: {
                    presets: ['env']
                }
            }
        }]
    }
};
```

`此时文件目录`
```node
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        2019/3/15     21:36                dist
d-----        2019/3/15     20:59                node_modules
d-----        2019/3/15     20:46                src
-a----        2019/3/15     20:59         171960 package-lock.json
-a----        2019/3/15     21:30            703 package.json
-a----        2019/3/15     21:30            139 rollup.config.js
-a----        2019/3/15     21:37            578 webpack.config.js
```

#####  [2.devtool](#top) <b id="target2"></b> 
* `eval`:`eval 模式会把每个 module 封装到 eval 里包裹起来执行，并且会在末尾追加注释。 这是 webpack 默认配置 这是不利于调试的 所以我们改变一下 
这个属性`
```node

/***/ "./src/index.js":
/*!**********************!*\
  !*** ./src/index.js ***!
  \**********************/
/*! no static exports found */
/***/ (function(module, exports, __webpack_require__) {

"use strict";
eval("\n\nvar sum = function sum(num1, num2) {\n  return.....");

/***/ })

/******/ });
```

```node
module.exports = {
    devtool:"eval",
    entry: {
        index: './src/index.js'
    },
  ...
```
* `source-map`:`他可以生成便于调试的文件`

```node
/***/ "./src/index.js":
/*!**********************!*\
  !*** ./src/index.js ***!
  \**********************/
/*! no static exports found */
/***/ (function(module, exports, __webpack_require__) {

"use strict";


var sum = function sum(num1, num2) {
  return num1 + num2;
};

var result = sum(30, 40);

console.log('tag', result);

/***/ })

/******/ });
//# sourceMappingURL=demo.min.js.map
```



#####  [3.package.json](#top) <b id="target3"></b> 

```json
{
  "name": "kicker-demo",
  "version": "1.0.1",
  "description": "demo to use webpack",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "product": "webpack --mode=production",
    "dev": "webpack --mode=development",
    "rollup": "rollup -c"
  },
  "repository": {
    "type": "git",
    "url": ""
  },
  "keywords": [
    "webpack-demo"
  ],
  "author": "jxkicker",
  "license": "ISC",
  "devDependencies": {
    "babel-loader": "^7.1.5",
    "babel-preset-es2015": "^6.24.1",
    "rollup": "^1.6.0",
    "webpack": "^4.29.6",
    "webpack-cli": "^3.2.3"
  },
  "dependencies": {
    "babel-core": "^6.26.3",
    "babel-preset-env": "^1.7.0"
  }
}

```

#####  [4.此时](#top) <b id="target4"></b> 
* `npm run dev`:`打包 开发环境`
* `npm run product`:`打包 生产环境`
* `npm rollup 打包文件`:`打包 合并源代码`



--------------------
`作者:` `模板` 
`完成时间`:`2019年3月15日21:43:34`
`备注信息`: `任意使用` 
