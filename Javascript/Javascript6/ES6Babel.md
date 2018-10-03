<a id="top"  href="#top">:arrow_lower_left: JavaScript6 Babel 环境配置 vscode :maple_leaf:</a>
----
`将ES6 转换为ES5的编译器`

- [x] <a href="#LetNodeStart">`安装 node 环境`</a>
- [x] <a href="#BabelrcFile">`配置.Babelrc文件`</a>
- [x] <a href="#UseBabel">`使用babel`</a>


#### 1.	:whale2: <a id="LetNodeStart" href="#LetNodeStart">node 安装</a>    <a href="#top">----:arrow_up::arrow_up: </a>

* `安装地址`: [`node 官方`](https://nodejs.org/zh-cn/)
```C#
  node -v 
  //dos 或者 powershell 输入  查看是否安装完毕
  npm -v 
  //查看 npm 是否安装完毕
  npm config set -g registry https://registry.npm.taobao.org
  //切换npm 镜像 不然下载贼慢
```
#### 1.	:whale2: <a id="BabelrcFile" href="#BabelrcFile">Babelrc 配置文件</a>    <a href="#top">----:arrow_up::arrow_up: </a>
* `增加一个.Babelrc 文件 内容如下`
```xml
{
  "presets": ["es2015"],
  "plugins": []
}
```
```node

 //初始化本地环境
 npm init
 
 //es2015转码规则
 npm install --save-dev babel-preset-es2015
 
 //react最新转码规则
 npm install --save-dev babel-preset-react
 
 //react最新转码规则
 npm install --save-dev babel-preset-latest
 
 // ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
 npm install --save-dev babel-preset-stage-0
 npm install --save-dev babel-preset-stage-1
 npm install --save-dev babel-preset-stage-2
 npm install --save-dev babel-preset-stage-3
 
 //需要什么安装什么 
 // 安装 babel-preset-es2015 那么需要在Babelrc 的presets 数组里面 添加  es2015
 // 安装 babel-preset-react 那么需要在Babelrc 的presets 数组里面 添加  react
 // ...
```

#### 1.	:whale2: <a id="UseBabel" href="#UseBabel">`使用babel`</a>    <a href="#top">----:arrow_up::arrow_up: </a>
```node

//安装 babel-cli 工具，用于命令行转码
npm install --global babel-cli

//执行转码
babel example.js -o compile.js --presets es2015

 实时监听编译文件：
$ babel example.js --watch -o compiled.js --presets es2015
```
