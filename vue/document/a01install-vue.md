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

##### :maple_leaf: [二.使用Vue](#top) <b id="usevue"></b>
* `通过CDN 引入 vue脚本`
   * `引入最新版 开发环境版本`:`<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>`
   * `引入最新版 生产环境版本`:`<script src="https://cdn.jsdelivr.net/npm/vue"></script>`
   * `引入 指定版本`:`<script src="https://cdn.jsdelivr.net/npm/vue@2.5.17/dist/vue.js"></script>`
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
