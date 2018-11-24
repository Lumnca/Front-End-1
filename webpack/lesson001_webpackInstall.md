### [Webpack 安装使用](#top) :maple_leaf: <b id="top"></b>

----
`Webpack 的入门使用方式 在开始之前，请确保安装了 Node.js 的最新版本。使用 Node.js 最新的长期支持版本(LTS - Long Term Support)，是理想的起步`
- [x] :maple_leaf: [`命令行安装`](#install) 
- [x] :maple_leaf: [`起步咯`](#start) 

##### [(一.1).命令行安装](#top) <b id="install"></b> :maple_leaf:
`-g 是全局安装的意思`
```npm
 cnpm install webpack -g
 
 webpack -v //查看安装的版本
```

##### [(一.2)本地安装](#top)
`要安装最新版本或特定版本，请运行以下命令之一：`
```npm
npm install --save-dev webpack
npm install --save-dev webpack@<version>
```
`如果你使用 webpack 4+ 版本，你还需要安装 CLI。`
```npm
npm install --save-dev webpack-cli
```
`对于大多数项目，我们建议本地安装。这可以使我们在引入破坏式变更(breaking change)的依赖时，更容易分别升级项目。通常，webpack 通过运行一个或多个 npm scripts，会在本地 node_modules 目录中查找安装的 webpack：`
```node
"scripts": {
    "start": "webpack --config webpack.config.js"
}
```
> `当你在本地安装 webpack 后，你能够从 node_modules/.bin/webpack 访问它的 bin 版本。`
##### [(一.3).基本配置](#top) :maple_leaf:
`webpack --mode production` :`打包成一行  生产环境`<br/>
`webpack --mode development`：`打包就可以了,开发环境`

##### [(二. 1).起步咯](#top) <b id="start"></b> :maple_leaf:
`首先我们创建一个目录，初始化 npm，然后 在本地安装 webpack，接着安装 webpack-cli（此工具用于在命令行中运行 webpack）：`
```linux
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```
(2).现在我们将创建以下目录结构、文件和内容：
```diff
  webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
src/index.js
```
