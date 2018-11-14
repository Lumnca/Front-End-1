[vue 列表渲染](#top) :maple_leaf: <b id="top"></b> 
----
`我们用 v-for 指令根据一组数组的选项列表进行渲染。v-for 指令需要使用 item in items 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。`

* :maple_leaf: [`数组列表`](#array) 
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
        <li v-for="(p,index) in persons" v-bind:key="index"  v-bind:style="{marginTop: marginlength + 'px'}" >
            <span class=" badge"> {{index}} </span> <label class="label label-danger" >{{p.name}}</labe> 
        </li>
    </ul>
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

    }
});
```
