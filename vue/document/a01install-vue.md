[Vue 安装 与 代码初体验 MVVM ](#top) <b id="top"></b> :maple_leaf:
-----
`vue安装 和初体验整理笔记理解mvvm 模式 model-view-viewModel 它是双向绑定的 通过 实现 数据绑定 和 Dom 监听 并且vue是声明式渲染 的框架`

##### :maple_leaf: [`一.安装 devtool 谷歌工具`](#top)   <b id="devtool"></b>
`这是十分有必要的一件事情,devtool可以很方便的帮助我们调试 vue项目代码` 

* `最简单安装`
  * `收缩网址:https://chrome.google.com/webstore/category/extensions`
  * `打开chrome 网上应用店 搜索 devtool 就行 然后添加就行`
  * `前提是你要有一个翻墙工具`
  
```c#
/* 源代码安装
devtool github: https://github.com/vuejs/vue-devtools
*/
git clone 下来

//然后运行命名

//初始化项目
cnpm install 

cnpm run build

//修改shells>chrome文件夹下的mainifest.json 中的persistant为true

//我们找到谷歌浏览器的扩展程序功能，勾选开发者模式

//然后我们将插件文件夹里的shells>chorme文件夹直接拖到页面中，完成安装。
```
* `本地启动它,需要一些操作 在扩展程序 里面找到 devtool里面的详细信息`
   * `允许访问文件网址` <br/> <br/>
![mvvm 模式图](/Resources/vue/devtool.png)

##### :maple_leaf: [二.使用Vue](#top) <b id="usevue"></b>
`Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。`
* `通过CDN 引入 vue脚本`
   * `引入最新版 开发环境版本`:`<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>`
   * `引入最新版 生产环境版本`:`<script src="https://cdn.jsdelivr.net/npm/vue"></script>`
   * `引入 指定版本`:`<script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>`
* `我们并不建议你一开始就是有vue-cli 脚手架 `   
   * `安装方法`:`npm install -g @vue/cli`
```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="http://code.jquery.com/jquery-migrate-1.2.1.min.js"></script>
    <!-- ....jquery bootstrap 引入文件 通过cdn 引入 网址: https://www.bootcdn.cn/twitter-bootstrap/  -->
</head>
<body class=" container">
    <br/>
    <div id="app">
        <input  type="text" v-model="name" class=" form-control " />
        <p>
            <label class="label label-primary">我的名称是: {{name}} </label> 
        </p>
        <button class="btn btn-danger btn-sm " v-on:click="showName(name)" >点击我啊</button>
    </div>
</body>
<script src="../vue-depend/vue.min.js"></script>
<script>
    const vm = new Vue({
        el:"#app",
        data:{
            name:"jxKicker",
            age:15,
            sex:true
        },
        methods:{
            showName:function(name){
                alert(name);
            }
        }
    });
</script>
</html>
```
**`样式如下:`** <br/>
![mvvm 模式图](/Resources/vue/example.png)
##### :maple_leaf: [`三.MVVM 模式 解释`](#top) <b id="mvvm"></b>
![mvvm 模式图](/Resources/vue/mvvm.png)
<br/>
`如上所示`
* `view:视图 html代码`
* `model:模型 数据`
* `view-model:视图模型 内部具有数据绑定 和dom 监听 实际上也可以想做是 vm 对象 入上面代码所示 就是我们写的vue代码`
* `vue 采用的模式 数据是双向绑定的,模型变了 视图跟随变化  视图变化 模型也跟着变化,中间的就是视图模型`
##### :maple_leaf: [`四.Vue 基本内容`](#top)   <b id="devtool"></b>
* `Vue 通过构造函数 Vue({option}) 创建一个Vue的实例 ` `let vm = new Vue({option})` `在实例化过程中,我们可以传入一个选项对象,包括数据 模板 
挂载元素,方法 生命周期钩子....`
* `el`:`字符串,选择器,挂载在何处`
