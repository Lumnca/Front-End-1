[Vue 安装 与 代码初体验 MVVM ](#top) <b id="top"></b> :maple_leaf:
-----
`vue安装 和初体验整理笔记理解mvvm 模式 model-view-viewModel 它是双向绑定的 通过 实现 数据绑定 和 Dom 监听`

##### :maple_leaf: [`一.安装 devtool 谷歌工具`](#top)   <b id="devtool"></b>
`这是十分有必要的一件事情,devtool可以很方便的帮助我们调试 vue项目代码` 

* `最简单安装`
  * `收缩网址:https://chrome.google.com/webstore/category/extensions`
  * `打开chrome 网上应用店 搜索 devtool 就行 然后添加就行`
  * `前提是你要有一个翻墙工具`
```c#
devtool github: https://github.com/vuejs/vue-devtools

git clone 下来

//然后运行命名

//初始化项目
cnpm install 

cnpm run build

//修改shells>chrome文件夹下的mainifest.json 中的persistant为true

//我们找到谷歌浏览器的扩展程序功能，勾选开发者模式

//然后我们将插件文件夹里的shells>chorme文件夹直接拖到页面中，完成安装。
```

##### :maple_leaf: [`三.MVVM 模式 解释`](#top) <b id="mvvm"></b>
![mvvm 模式图](Resources/vue/mvvm.png)
