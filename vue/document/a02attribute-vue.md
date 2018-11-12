[Vue 数据属性 ](#top) <b id="top"></b> :maple_leaf:
-----
`Vuew 数据属性体验 {{}} ` `v-text` `v-html` `计算属性` `监视`

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
