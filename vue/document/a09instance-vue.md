### [vue 实例方法和属性](#top) <b id="top"></b>
----
[`官方API`](https://cn.vuejs.org/v2/api/#vm-data)

------

- [x] [`1.vue 实例属性`](#target1)
- [x] [`2.vue 实例方法 / 数据`](#target2)


------

#####  [1.vue 实例的属性](#top) <b id="target1"></b> 
* `vm.$data`:`Vue 实例观察的数据对象。Vue 实例代理了对其 data 对象属性的访问。`
* `vm.$props`:`当前组件接收到的 props 对象。Vue 实例代理了对其 props 对象属性的访问。`
* `vm.$el`:`Vue 实例使用的根 DOM 元素。 挂载在哪里`
* `vm.$options`：`用于当前 Vue 实例的初始化选项。需要在选项中包含自定义属性时会有用处：`

   ```node
    //用于自定义属性
    new Vue({
      customOption: 'foo',
      created: function () {
        console.log(this.$options.customOption) // => 'foo'
      }
    })
   ```
* `vm.$parent`:`当前组件树的根 Vue 实例。如果当前实例没有父实例，此实例将会是其自己。`
* `vm.$root`:`当前实例的直接子组件 但是不保证返回子组件的顺序`
* `vm.$children`:`父实例，如果当前实例有的话。`
* `vm.$slots`:[`官方解释`](https://cn.vuejs.org/v2/api/#vm-slots)
* `vm.$scopedSlots`
* `vm.$refs`:`一个对象，持有注册过 ref 特性 的所有 DOM 元素和组件实例。`
   ```node
    <div id="items">
        <h2 v-once >{{title}} <small ref="subTitle">这是子标题</small> </h2>
    </div>

    var items = new Vue({
      el:"#items",
      data:{
          count:0,
          title:"数据列表"
      }
    });
    //获得small 子标题
    console.log('子标题:', items.$refs.subTitle)
    //子标题: <small>这是子标题</small>
   ```
* `vm.$isServer`:`当前 Vue 实例是否运行于服务器。 返回Boolean`
* `vm.$attrs`
* `vm.$listeners`



#####  [2.vue 实例方法 / 数据](#top) <b id="target2"></b> 
* `vm.$nextTick( [callback] )`:`等待Dom 更新完之后在执行callback 函数 因为Dom 的更新是需要时间的,不然在没有更新的时候去取得
vm的值可能取得旧值`
```node
new Vue({
  // ...
  methods: {
    // ...
    example: function () {
      // 修改数据
      this.message = 'changed'
      // DOM 还没有更新
      this.$nextTick(function () {
        // DOM 现在更新了
        // `this` 绑定到当前实例
        this.doSomethingElse()
      })
    }
  }
})
```
* `vm.$set( target, key, value )`:`这是全局 Vue.set 的别名。给实例增加新的属性`

   * `通过这样的方法添加的属性可以实时监控` `通过this.user.age = 18; 这样的方法添加实现无法实现数据监控`
   
   ```node
     <div id="test">
        <button v-on:click="addAgeByPoint()">添加年龄</button>
        <button v-on:click="addAgeBy$set()">添加年龄</button>
        <h2 v-text="user.name"></h2>
        <h2 v-text="user.age"></h2>
        <h2 v-text="user.sex"></h2>
    </div>
    
    var test = new Vue({
        el:"#test",
        data:{
            user:{
                name:'JxKicker'
            }
        },
        methods: {
            addAgeByPoint(){
                this.user.age = 18;
                console.log(this.$data);
            },
            addAgeBy$set(){
                this.$set(this.user,'sex',"男");
                console.log(this.$data);
            }    
        },
     })

   ```
* `vm.$watch( expOrFn, callback, [options] )`:`监视器 观察 Vue 实例变化的一个表达式或计算属性函数。回调函数得到的参数为新值和旧值。
表达式只接受监督的键 路径。对于更复杂的表达式，用一个函数取代。`
   
    * `也可以通过vue的 watch 属性在里面监视`
    
    ```node
    watch: {
      firstName: function (newValue,newValue) {
        this.fullName = val + ' ' + this.lastName
      },
      lastName: {
        handler: function (newValue,newValue) {
          this.fullName = this.firstName + ' ' + val
        },
        deep:true
      }
    }
    ```
    
    ```node
      <div id="update">
          <input type="text" v-model="name">
      </div>
      var update = new Vue({
          el:"#update",
          data:{
              name:"tom",
              age:23
          }
      });
      update.$watch('name',function(newValue,oldValue){
          console.log('newvalue', newValue);
          console.log('oldvalue',oldValue);
      },{
          immediate: true
      });
   ```
   
   ``` 
    选项：deep 监视引用是否更改 不加它是监视值是否修改

    为了发现对象内部值的变化，可以在选项参数中指定 deep: true 。注意监听数组的变动不需要这么做。

    vm.$watch('someObject', callback, {
      deep: true
    })
    vm.someObject.nestedValue = 123
    // callback is fired

    选项：immediate

    在选项参数中指定 immediate: true 将立即以表达式的当前值触发回调：

    vm.$watch('a', callback, {
      immediate: true
    })
    // 立即以 `a` 的当前值触发回调
  ```

* `vm.$delete( target, key )`:`这是全局 Vue.delete 的别名。删除属性`
   
   ```node
    doDelete$delete(){
        this.$delete(this.user,"name");
    }
   ```


--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `任意使用` 
