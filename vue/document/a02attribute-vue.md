[`Vue 数据属性` ](#top) <b id="top"></b> :maple_leaf:
-----
`Vue 数据属性体验 {{}} ` `v-text` `v-html` `计算属性` `监视`

- [x] [`vue 数据绑定语法`](#bind)
- [x] [`vue 计算属性`](#calcul)

#### :maple_leaf: [零.数据](#top)
`Vue 实例中可以通过data属性定义数据,这些数据可以在实例对应的模板中进行绑定并使用`
* `需要注意的是,如果传入data的是一个对象,Vue实例会代理起对象里面所有的属性,而不是对传入的对象进行深拷贝`
* `我们可以通过` `vm.$data` `来获取生命的数据 通过` `{{propertyName}}` `来输出属性的值 如果修改属性的值 那么模板中的数据也会变化,这就叫`
`响应式数据`
* `注意`:`只有初始化时传入的对象才是响应式的,如果在声明实例后再添加一个属性  那么这个属性不是响应式并且抛出异常`
* `所以我们应该尽量在初始化的时候,吧所有的变量都设定好,如果没有值,也可以用undefined 或null 占位`
* `组件类型的实例可以通过props来获取数据,和data一样`
```html
<body class="container">
    <br/>
    <div id="app">
        <label class=" label label-danger">{{name}}</label>
        <val-list title="这是标题一"  content="这是内容一" ></val-list>
        <val-list title="这是标题二"  content="这是内容二" ></val-list>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
let myComponent = Vue.component('val-list',{
  props:[ 'title','content'],
  template:`<h3>{{title}} <small>{{content}}</small></h3>`
});
//使用组件
new Vue({ 
  el: '#app',
  data:{
      name:"这是组件"
  }  
 })
</script>
```
* `在组件内部可以使用data 声明数据,一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝` **`重要的一句话`**
```html
<div id="app">
    <label class=" label label-danger">{{name}}</label>
    <val-list title="这是标题一"  content="这是内容一" ></val-list> 
    <val-list title="这是标题二"  content="这是内容二" ></val-list>
</div>
let myComponent = Vue.component('val-list',{
  props:[ 'title','content'],
  data: function () {
    return {count: 0}
  },
  methods:{
      add:function(){
          this.count++;
      }
  },
  template:
  `<div style="cursor: pointer;">
        <h3 v-on:click="add">{{title}} <small>{{content}}</small> </h3> 
        <label class=" label label-danger"> {{count}} </label>
   </div>
  `
});
//使用组件
new Vue({ 
   el: '#app',
   data:{
      name:"这是组件 点击试一试"
   }  
})

```
[`通过 Prop 向子组件传递数据`](#top)
```html
<div id="post">
     <blog-post v-for="post in posts" v-bind:key="post.id" v-bind:count="post.id" v-bind:title="post.title" >
    </blog-post>
</div>
<script>
Vue.component('blog-post', {
    props: ['title','count'],
    template: '<h3><label class=" label label-primary">{{ title }} --- {{count}}</label>   </h3>'
});
new Vue({
    el: '#post',
    data: {
        posts: [
        { id: 1, title: 'My journey with Vue' },
        { id: 2, title: 'Blogging with Vue' },
        { id: 3, title: 'Why Vue is so fun' }
        ]
    }
});
</script>
```
##### :maple_leaf: [一.普通属性绑定](#top)
`当一个 Vue 实例被创建时，它向 Vue 的响应式系统中加入了其 data 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会
产生“响应”，即匹配更新为新的值。`
* `v-hmtl`:`渲染为 innerHtml`
* `v-text`:`渲染为 `
```html
<body class="container">
    <br/>
    <div class=" row">
        <div id="val" class=" col-md-12" >
            <h3>属性绑定</h3>
            <span class=" label label-info">姓名:</span> <input type="text" v-model="name"> <br/>
            <span class=" label label-info">年龄:</span> <input type="text" v-model="age"> <br/>
            <span class=" label label-info">性别:</span> <input type="text" v-model="sex"> <br/>

            <hr/>
            <p>
                <label class=" label label-primary">姓名:</label> <span>{{name}}</span>
                <label class=" label label-primary">年龄:</label> <span>{{age}}</span>
                <label class=" label label-primary">性别:</label> 
                <span v-if="sex == '男'">男</span> 
                <span v-else >女</span> 
            </p>
            <p v-html="loginBtn">
                
            </p>
            <p v-text="message" class=" text-muted"></p>
        </div>
    </div>
    
</body>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let person = new Vue({
        el:"#val",
        data:{
            name:"Jxkicker",
            age:18,
            sex:'男',
            loginBtn: "<a href='https://www.baidu.com' class='btn btn-sm btn-default' > 立即登录</a>",
            message:"请填写你的个人基本信息,我们将严格保密你的信息"
        }
    });
</script>
```
#### :maple_leaf: [二.Vue 数据绑定语法](#top) <b id="bind"></b>
`Vue.js 使用了基于 HTML 的模板语法 数据绑定具有多种方法 ` `在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。` 
* `插值绑定 {{}} v-once`
* `原始 HTML`
* `HTML 特性 v-bind`
* `使用 JavaScript 表达式`
* `修饰符`
##### [插值绑定](#top)
`通过使用` `v-once` `指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。但请留心这会影响到该节点上的其它数据绑定：`

```html
<span>Message: {{ msg }}</span>

<span v-once>这个将不会改变: {{ msg }}</span>
```
##### [原始 HTML](#top)
`双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用` `v-html` `指令：`

```html
<span v-html="rawHtml"></span></p>
//这个 span 的内容将会被替换成为属性值 rawHtml
```
##### [HTML 特性](#top)
`Mustache 语法不能作用在 HTML 特性上，遇到这种情况应该使用 v-bind 指令：`
```html
<div v-bind:id="dynamicId"></div>
<button v-bind:disabled="isButtonDisabled">Button</button>

<a v-bind:href="url">...</a> //url为属性
```
* `v-bind 缩写`
```html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
```
##### [使用 JavaScript 表达式](#top)
```html
//age 属性是否大于 18
<span v-if="age >= 18" ></span>
```
##### [filter 过滤器](#top)
`Vue.js 允许你自定义过滤器` `{{name | capitalize | uppercase }}` `通过 管道 |可以定义多个过滤器` 
```html
<div class=" row">
    {{name | capitalize }}
</div>
<script>  
    let val = new Vue({
        el:".row",
        data:{
            name:"jxKicker"
        },
        filters: {
            capitalize: function (value) {
                if (!value) return ''
                value = value.toString()
                return value.charAt(0).toUpperCase() + value.slice(1)
            }
        }
    });
</script>
```
##### [修饰符 事件](#top)
`修饰符 (Modifiers) 是以半角句号 . 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()：`
```html
<form v-on:submit.prevent="onSubmit">...</form>
```
`v-on 绑定事件 缩写语法 @`
```html
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
```
##### :maple_leaf: [三.vue 计算属性](#top) <b id="calcul"></b>
`模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。例如：`
```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    