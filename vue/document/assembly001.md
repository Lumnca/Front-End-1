### [vue 组件 01](#top) <b id="top"></b> 

----
`至此才是vue的起步 组件`


-----
- [x]  [`介绍`](#intro)
- [x]  [`简单小例子`](#exp)
- [x]  [`配置参数`](#set)
- [x]  [`传递数据`](#data)

#####  [Vue 组件介绍](#top)  <b id="intro"></b>  
`组件是Vue.js 最核心的功能,也是整个框架设计最精彩的地方,当然也是最难掌握的。`
* `组件是可复用的 Vue 实例，且带有一个名字`
* `组件在渲染时 会用 template 内容代替原来的组件标签`
`组成一个组件 全局注册`
```node
Vue.component('first-componet',{
    //配置组件选项
});
```
#####  [Vue 简单小例子](#top)  <b id="exp"></b>
```html
<div id="val">
    <first-componet></first-componet>
    <first-componet></first-componet>
</div>
```
```node
Vue.component('first-componet', {
    //配置组件选项
    data:function(){
        return {
            index:1,
            message:"请点击我吧"
        }
    },
    template:"<button class='btn btn-sm btn-primary'>{{index}} {{message}}</button>"
});

let vals = new Vue({
    el:"#val"
});
```
`渲染结果`
```html
<div id="val">
  <button class="btn btn-sm btn-primary">1 请点击我吧</button>
  <button class="btn btn-sm btn-primary">1 请点击我吧</button>
</div>
```
#####  [配置参数说名](#top)  <b id="set"></b> 
* `data 属性必须是函数 为什么 因为组件可以复用使用函数 可以让每个组件都具有自己的data属性  不然就多个组件共用一个data 对象 然后
一个改变 其他都改变 可以返回一个对象`
```node
data: function (){
  return { count: 0 };
}
```
* `template:属性的Dom结构必须被一个元素包含,如果直接写出 <span>...</span><b>...</b> 是不会渲染成功的`
* `vue的组建的末班在某些情况下会受到HTML的限制,比如table内规定只允许是 tr td th等表格元素 所以在table内直接使用组件是无效的 这种情况下要使用
` **`is`** `属性来挂载组件`

```html
  <table class=" table table-hover">
      <caption>这是一个例子</caption>
      <tbody  >
          <tr is="my-row" age="12" uname="蒋星" sex="男" uid="2016110418" ></tr>
      </tbody>
  </table>
```
```node
Vue.component('my-row',{
    props:['age','sex','uid','uname'],
    template:`
        <tr>
            <td>{{age}}</td> 
            <td>{{sex}}</td> 
            <td>{{uid}}</td> 
            <td>{{uname}}</td>   
            <td><first-componet></first-componet></td> 
        </tr>
    `
})
```
```html
<table class=" table table-hover">
  <caption>这是一个例子</caption> 
  <tbody>
    <tr>
      <td>12</td> 
      <td>男</td> 
      <td>2016110418</td> 
      <td>蒋星</td> 
      <td><button class="btn btn-sm btn-primary">1 请点击我吧</button></td>
    </tr>
  </tbody>
</table>
```

#####  [传递数据](#top)  <b id="data"></b> 
`vue组件有很多数据流转 比如父组件和子组件之间 组件之前通信 主要是 父组件向子组件传递数据 子组件根据参数的不同来渲染不同的内容或执行操作 `
* `data: 让每个vue具有自己的数据 他来自于自己`

##### 利用props 传递数据
`props的值可以是两种,一种是字符串数组,一种书对象 props的数组 来自于父组件`
##### 字符串数组
`可以由父组件绑定 也可以手动传参`
```html
<div id="val">
    <person-info-componet
          v-for="p in persons" 
          :key=p.id  :name = p.name :age = p.age  :id=p.id>
    </person-info-componet>
    <person-info-componet name="LiZhiMing" age="15" id="2016110425" ></person-info-componet>
</div>
```

```node
Vue.component('person-info-componet', {
    props:["name","age","id"],
    template:`
        <div>
            <span class="text-danger"> {{ id }} </span>
            <span class="text-danger"> {{ age }} </span>
            <span class="text-danger"> {{ name }} </span>
        </div>
    `
});


let vals = new Vue({
    el:"#val",
    data:{
        count:3,
        persons:[
            { name:"Jxkicker",age:20,id:"2016110418"},
            { name:"Ljk",age:20,id:"2016110423"},
            { name:"JLZ",age:22,id:"2016110417"}
        ]
    }
});
```












