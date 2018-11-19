### [vue 表单收集](#top) :maple_leaf: <b id="top"></b> 

----
`vue 表单输入绑定 提供了 v-model可以自动收集表单信息 v-model 创建双向数据绑定 本质只是一种语法糖 它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。`

- [x] :maple_leaf: [`文本绑定`](#text)
- [x] :maple_leaf: [`复选框`](#check)
- [x] :maple_leaf: [`单选按钮`](#radio)
- [x] :maple_leaf: [`选择框`](#options)
- [x] :maple_leaf: [`绑定值`](#bind)
- [x] :maple_leaf: [`修饰符`](#desc)


##### [文本绑定](#top)  :maple_leaf: <b id="text"></b> 
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
       <option disabled value="">请选择</option>
      <option v-for="(item,index) in UserCitys" :value="item.id"  :key="item.id" >{{ item.name }}</option>
  </select>
```
> `如果 v-model 表达式的初始值未能匹配任何选项，<select> 元素将被渲染为“未选中”状态。在 iOS 中，这会使用户无法选择第一个选项。因为这样的情况下，iOS 不会触发 change 事件。因此，更推荐像上面这样提供一个值为空的禁用选项。`
```node
  data:{
    UserCitys:[{id:1,name:"贵州"},{id:2,name:"北京"},{id:3,name:"沈阳"},{id:4,name:"南京"}],
    city:""
  }
```
`多选时 值绑定到数组中`
```html
 <label for="grade" >历史成绩:</label>
 <select id="grade" v-model="Grades" multiple >
    <option v-for="(item,index) in UserGrades" :value="item"  :key="index" >{{ item }}</option>
 </select>
```
```node
  UserGrades:[68.6,96.5,95.6,88,94],
  Grades:[]
```
##### [绑定值](#top)  :maple_leaf: <b id="bind"></b> 
`我们可以通过v-bind 给表单空间绑定值 绑定的值可以是 基本类型数据 也可以是对象`

```html
<input type="radio" v-model="pick" v-bind:value="a">
// 当选中时
vm.pick === vm.a

<select v-model="selected">
    <!-- 内联对象字面量 -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
// 当选中时
typeof vm.selected // => 'object'
vm.selected.number // => 123
```

##### [修饰符](#top)  :maple_leaf: <b id="desc"></b> 
* .lazy:`在默认情况下，v-model 在每次 input 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。你可以添加 lazy 修饰符，从而转变为使用 change 事件进行同步：`
```html
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >
```
* .number:`如果想自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符：`
   * `这通常很有用，因为即使在 type="number" 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 parseFloat() 解析，则会返回原始的值。`
```html
<input v-model.number="age" type="number">
```
* `.trim`:`如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：`
```html
<input v-model.trim="msg">
```





















