### [vue 表单收集](#top) :maple_leaf: <b id="top"></b> 

----
`vue 表单输入绑定 提供了 v-model可以自动收集表单信息 v-model 创建双向数据绑定 本质只是一种语法糖 它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。`

- [x] :maple_leaf: [`文本绑定`](#text)
- [x] :maple_leaf: [`复选框`](#check)
- [x] :maple_leaf: [`单选按钮`](#radio)
- [x] :maple_leaf: [`选择框`](#options)
- [x] :maple_leaf: [`系统修饰键`](#system)


##### [文本绑定](#top)  :maple_leaf: <b id="array"></b> 
> 很简单 使用 `v-model` 命令实现双向绑定就行 

```html
    <div class=" row">
        <div id="val" class=" col-md-12" >
            <form id="user"  v-on:submit.prevent="submitHandler($event)" >
                <label class=" label label-primary" for="username">账号</label>
                <input type="text" id="username" v-model="userId" > <br/><br/>
                <label class=" label label-primary" for="username">密码</label>
                <input type="text" id="username" v-model="userPassword" >
                <br/><br/>

                <span>用户描述:</span>
                <p style="white-space: pre-line;">输入:{{ message }}</p>
                <br>
                <textarea
                 v-model="message" 
                 :style="{ width: widthAre + 'px',height:heightAre + 'px' }"
                ></textarea>
                <br>
                <input type="submit" value="立即提交" class=" btn btn-sm btn-primary" />
            </form>
        </div>
    </div>
```

```node
    let person = new Vue({
        el:"#val",
        data:{
            userId:"",
            userPassword:'',
            message:"",
            widthAre:300,
            heightAre:100
        },
        methods:{
            submitHandler:function(event){
                console.log(this.userId,this.userPassword,this.message);
            }
        }
    });
```
##### [复选框](#top)  :maple_leaf: <b id="check"></b> 
> `v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 data 选项中声明初始值。`

`单个复选框，绑定到布尔值：`

```html
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```
```node
  data:{
      userId:"",
      userPassword:'',
      message:"",
      widthAre:300,
      heightAre:100,
      isChoose:true
  },
```
`多个复选框，绑定到同一个数组：`
```html
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
```

```node
 data:{
   checkedNames:["Jack"] //先选中第一个
 }
```
##### [单选按钮](#top)  :maple_leaf: <b id="radio"></b> 
```html
  <div>
      <input type="radio" id="girl" value="girl" v-model="userSex">
      <label for="girl">男</label>
      <input type="radio" id="boy" value="boy" v-model="userSex">
      <label for="boy">女</label>
      <br>
      <span>用户性别: {{ userSex }}</span>
  </div>
```

```node
  userSex:""
```

##### [选择框](#top)  :maple_leaf: <b id="options"></b> 
`单选时`

```html
  <label for="cityID" >城市:</label>
  <select id="cityID" v-model="city">
      <option v-for="(item,index) in UserCitys" :value="item.id"  :key="item.id" >{{ item.name }}</option>
  </select>
```
```node
  data:{
    UserCitys:[{id:1,name:"贵州"},{id:2,name:"北京"},{id:3,name:"沈阳"},{id:4,name:"南京"}],
    city:""
  }
```
`多选时`
```html

```





























