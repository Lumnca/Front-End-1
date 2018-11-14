[vue 列表渲染](#top) :maple_leaf: <b id="top"></b> 
----
`我们用 v-for 指令根据一组数组的选项列表进行渲染。v-for 指令需要使用 item in items 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。`

* :maple_leaf: [`数组列表`](#array)
* :maple_leaf: [`数组更新检测`](#array)
* :maple_leaf: [`对象渲染`](#object)
* :maple_leaf: [`key 问题`](#key)

##### [数组渲染](#top)  <b id="array"></b> 
`数组渲染` `在 v-for 块中，我们拥有对父作用域属性的完全访问权限。`
```html
<ul class=" list-unstyled">
    <li v-for="p in persons" :key="p.id">
        <label class="label label-danger" >{{p.name}}</labe>
    </li>
</ul>
```
* `v-for 还支持一个可选的第二个参数为当前项的索引`
```html
<div id="val">
    <ul class=" list-unstyled">
        <li v-for="(p,index) in persons" v-bind:key="index" 
            v-bind:style="{marginTop: marginlength + 'px'}" >
            <span class=" badge"> {{index}} </span> 
            <label class="label label-danger" >{{p.name}}  {{p.age}}</labe> 
            <input type="radio"   v-model="p.sex"  value="true"   >男
            <input type="radio"   v-model="p.sex" value="false" >女
            {{p.sex}}
        </li>
    </ul>
    <button @click="update" class="btn btn-sm btn-primary">保存修改</button>
</div>
```
```node
let person = new Vue({
    el:"#val",
    data:{
        marginlength:"5",
        persons:[
            {name:"kicker",age:15,sex:true},
            {name:"Jom",age:19,sex:true},
            {name:"Tome",age:18,sex:false},            
            {name:"Tony",age:14,sex:false}
        ]          
    },
    methods:{
        update:function(){
            alert("已经保存在服务器...");
        }
    }
});
```
![结果图](/Resources/vue/for-array.png)

##### [`数组更新检测`](#array)
`Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下：`
* push()
* pop()
* shift()
* unshift()
* splice()
* sort()
* reverse()
##### [对象渲染](#top)  <b id="object"></b> 
`1. 一参数渲染 值`
```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```
`2. 二参数渲染 值键对`
```html
<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>
```
##### 实例 
```html
<div id="obj">
    <ul class=" list-unstyled">
        <li v-for="(value,key) in object" v-bind:key="key">
            {{key}}:{{value}}
        </li>
    </ul>
</div>
```
```node
new Vue({
    el: '#obj',
    data: {
        object: {
        firstName: 'John',
        lastName: 'Doe',
        age: 30
        }
    }
});
```
![结果图](/Resources/vue/for-object.png)

##### [key 问题](#top)  <b id="key"></b> 
* `当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。这个类似 Vue 1.x 的 track-by="$index" 。`
* `这个默认的模式是高效的，但是只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出。`
```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```
