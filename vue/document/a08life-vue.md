### [vue 生命周期](#top) <b id="top"></b> 

----
`每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：它进过了 从创建到 更新 再到死亡这三个大的生命周期过程 每一个vue实例都有一系列的初始化步骤
例如建立数据库,创建数据绑定,再次过程中我们可以通过一些定义好的生命周期钩子函数来运行业务逻辑`

- [x] [`1.三个大的阶段`](#process)
- [x] [`2.生命周期钩子`](#hook)
- [x] [`3.有用的钩子函数`](#useful)
- [x] [`4.注意了`](#notice)
- [x] [`5.与生命周期有管的API`](#target5)


##### [1.三个大的阶段](#top)  <b id="hook"></b> 
`基本是一个vue实例都经过三个大的过程` `初始化显示` `更新显示` `死亡`

##### [2.生命周期钩子](#top)  <b id="process"></b> 
`每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。
同时在这个过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。`
* `比如 created 钩子可以用来在一个实例被创建之后执行代码：`

<img src="https://cn.vuejs.org/images/lifecycle.png" width = "500" />


##### [3.有用的钩子函数](#top)   <b id="useful"></b> 
`主要关心那几个状态就行`
* `beforeCreate`:`在vue实例开始初始化时同步调用,此时数据观测,事件等尚未初始化`
* `created`:`实例已经创建，此时已经完成数据绑定事件方法,但是尚未开始DOM编译 就是vue尚未挂载到 dom中`
* `beforeMount`:`挂载之前调用`
* `mounted`:`挂载后调用的函数`
* `beforeUpdate`:`更新之前调用`
* `updated`:`更新之后调用`
* `beforeDestroy`:`在vue实例销毁之前调用`
* `destroyed`:`实例销毁后调用`

##### [4.注意了](#top)  <b id="notice"></b> 
`不要在选项属性或回调上使用箭头函数` `比如 created: () => console.log(this.a) 或
vm.$watch('a', newValue => this.myMethod())。` `因为箭头函数是和父级上下文绑定在一起的，this
不会是如你所预期的 Vue 实例，` `经常导致` <br/>
`Uncaught TypeError: Cannot read property of undefined` <br/>
`或`  <br/>
`Uncaught TypeError: this.myMethod is not a function 之类的错误。` <br/>

* `在钩子函数里面 对于定时器要使用 箭头函数 不然无法触发定时器函数改变值 因为普通函数this指向运行时的环境`
* `且注意销毁定时器对象 以防止内存泄漏`
```node
    let person = new Vue({
        el:"#val",
        data:{
            isShow:true,
            Internal:null
        },
        beforeCreate() {
            console.log("vue 正在构建实例");
        },
        created(){
            this.Internal = window.setInterval(()=>{
                this.isShow = !this.isShow;
            },500);
            console.log("vue 已经完成实例构建")
        },
        mounted(){
            console.log('Vue 实例已经挂载到DOM上面');
        },
        destroyed() {
            clearInterval(this.Internal);
            console.log('Vue 已经销毁');
        },
        
    });
```
##### [5.与生命周期有管的API](#top)  <b id="target5"></b> 
* `vm.$mount( [elementOrSelector] )`:`vm 是 vue实例`

    > `如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用 vm.$mount() 手动地挂载一个未挂载的实例。`
    ```node
    var MyComponent = Vue.extend({
      template: '<div>Hello!</div>'
    })

    // 创建并挂载到 #app (会替换 #app)
    new MyComponent().$mount('#app')

    // 同上
    new MyComponent({ el: '#app' })

    // 或者，在文档之外渲染并且随后挂载
    var component = new MyComponent().$mount()
    document.getElementById('app').appendChild(component.$el)
    ```
* `vm.$forceUpdate()`
    > `迫使 Vue 实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。`
    
* `vm.$nextTick( [callback] )`

    > `将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。它跟全局方法 Vue.nextTick 一样，不同的是回调的 this 自动绑定到调用它的实例上。`
    
* `vm.$destroy()`

   > `完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器。`
    













