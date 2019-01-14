### [Webpack 打包第二课](#top) :herb: <b id="top"></b>

-----
`很简单的,不要怕麻烦,这都是刚需,你有啥办法是不是！来吧从4.28.2 起4.0开始

- [x] [`1.安装环境`](#use) 
- [x] [`2.开始配置`](#node) 
- [x] [`3.添加Rollup`](#roll) 
- [x] [`4.多个入口点`](#in) 

-------
##### :triangular_flag_on_post: [1.安装环境](#top) <b id="use"></b> 
* `基本操作：`
  * `一个空的目录文件下面`
  * **`1.cnpm init `** :`或者:npm init -y  【-y】 的意思:Generate it without having it ask any questions:`
  * **`2.cnpm install webpack webpack-cli --save-dev `** :`webpack-cli:webpack 命令需要`
  * `基本的环境搞定`
  
##### :triangular_flag_on_post: [2.使用配置文件](#top) <b id="node"></b> 
`根目录使用 新建配置文件 webpack.config.js 并配置输出模式`
```node
const path = require('path');

module.exports = {
  entry: './src/index.js',
  mode: 'development', //mode: 'production',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};

```
`运行命令`
```node
npx webpack --config webpack.config.js
```
##### 命令行指定开发模式
`在package.json 中增加两个命名`
```node
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "product":"webpack --mode=production",
  "dev":"webpack --mode=development"
},
```
* `npm run dev `：`打包结果为开发模式`
* `npm run product`:`生产模式 min`

##### :triangular_flag_on_post: [3.添加Rollup](#top) <b id="roll"></b> 
```node
npm install --save-dev rollup
```
`添加配置文件`
```node
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
};
```
`添加命令`
```c#
 "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1",
   "product": "webpack --mode=production",
   "dev": "webpack --mode=development",
   "rollup": "rollup -c"
 }
```
##### :triangular_flag_on_post: [4.多个入口点](#top) <b id="in"></b> 
```node
const path = require('path');

module.exports = {
  entry: {
     app: './src/index.js',
     git:"./src/git.js"
  },
  output: {
    filename: '[name].js',
    path: path.resolve(__dirname, 'dist')
  }
};

```
