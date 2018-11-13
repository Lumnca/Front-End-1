### [Vue Class 与 Style 绑定](#top) <b id="top"></b> :maple_leaf:

-----
`操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是属性，所以我们可以用 v-bind 处理它们：只需要通过表达式计算出字符串结果即可。
不过，字符串拼接麻烦且易错。因此，在将 v-bind 用于 class 和 style 时，Vue.js 做了专门的增强。`
>`表达式结果的类型除了字符串之外，还可以是对象或数组。`

##### :maple_leaf: [`一.绑定字符串-Class`](#top)
* `将字符串样式 利用 v-bind 绑定`
```html
<div id="cstyle">
    <p v-bind:class="UserStyle"  >修改样式的方式</p>
    <!-- 结果: <p class="aClass cClass">修改样式的方式</p> -->
    <p v-bind:class="UserStyle" class="bcClass"  >绑定多个样式</p>
    <!-- 结果: <p class="bcClass bClass">绑定多个样式</p> -->
    <button v-on:click="update" class=" btn btn-sm btn-danger">修改样式</button>
</div>
```
[`vue 代码`](#top)
```node
let vm = new Vue({
    el:"#cstyle",
    data:{
        bcStyle:"bcClass",
        UserStyle:"aClass cClass",
    },
    methods:{
        update:function(){
            this.UserStyle = "bClass"; //可以动态修改
        }
    }
});
```
##### :maple_leaf: [`二.绑定对象-Class -对象语法`](#top)
`将类名和布尔值结合起来使用` 
* `<div v-bind:class="{ active: isActive }"></div>`
* `第二种`:`<div v-bind:class="classObject"></div>`

```node
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```
```html
<div id="cstyle">
    <p v-bind:class="{ aClass:hasA,cClass:hasC }"  >修改样式的方式</p>
</div>
<button v-on:click="update" class=" btn btn-sm btn-danger">修改样式</button>
```
[`vue 代码`](#top)
```node
let vm = new Vue({
    el:"#cstyle",
    data:{
        hasA:false,
        hasC:false,
    },
    methods:{
        update:function(){
            this.hasA =true;
            this.hasC =true;
        }
    }
});
```
##### :maple_leaf: [`三.绑定一个对象-Class -数组语法`](#top)
`我们可以把一个数组传给 v-bind:class，以应用一个 class 列表：`
```html
<div v-bind:class="[activeClass, errorClass]"></div>
<!--渲染结果: <div class="active text-danger"></div> -->
```
[`vue 代码`](#top)
```javascript
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```
##### :maple_leaf: [`四.绑定Style-Style `](#top)
`绑定style的样式名称 要把-去除掉 使用js样式名`
```html
<div id="cstyle">
    <p v-bind:style="{color:activeColor,fontSize:fontSize + 'px' }">你们好啊，来看看新的样式吧！</p>
    <button v-on:click="update" class=" btn btn-sm btn-danger">修改样式</button>
</div>
```
[`vue 代码`](#top)
```node
let vm = new Vue({
    el:"#cstyle",
    data:{
        activeColor:"red",
        fontSize:17
    },
    methods:{
        update:function(){
            this.activeColor = "green";
            this.fontSize = 25;
        }
    }
});
```
##### :maple_leaf: [`五.组件样式 `](#top)
`组件的属性小写敏感 下面应该用 users 而不是 usersClass 这样绑定会失效 vue推荐使用一个单词的小写`
```html
<div id="val">
    <person v-bind:users="usersClass" v-bind:user="userClass" ></person>
</div>
```
[`vue 代码`](#top)
```node
let per = Vue.component("person", {
    props: ['users','user'],
    template:
    `<div v-bind:class="users">
        你们好啊
        <span class="lable label-danger">{{user}}</span>
    </div>`
});

let users = new Vue({
    el:"#val",
    data:{
        usersClass:"bcClass",
        userClass:"bClass"
    }
}); 
```
