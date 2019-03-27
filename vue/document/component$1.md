##### 1.什么是组件 ?
`组件（Component）是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素， Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。
使用组件`

##### 2.创建组件--组件构造器
1. `约束:template 必须有一个根元素 有且只有一个`
2. `组件中 name 属性可以指定组件的名称 打开 vue-devtools 就可以看见了`
3. `template 可以是html字符串 也可以是一个 Id名称 template 标签的id `
4. `例子: template.html`

* 1.使用 API: Vue.extend( options )

```javascript
/*先定义组件配置*/
var labHeader = Vue.extend({
  name:"userinfo12501",
  template: `
      <div>
          <div><small>姓名: <span>{{uName}}</span></small></div>
          <div><small>年龄: <span>{{uAge}}</span></small></div>
      </div>
  `,
  data: function () {
      return {
          uName: 'Walter',
          uAge: 19,
      }
  }
});

/*再给组件一个 html 标签名称*/
Vue.component("user-label", labHeader);
```
> `可以简写为:`  `Vue.component('my-component', Vue.extend({ ... }))`
* 2.使用 API：Vue.component( id, [definition] ) 
```javascript
<div id="demo">
  <user-label></user-label>
</div>

Vue.component("user-label", {
  template: `
      <div>
          <div><small>姓名: <span>{{uName}}</span></small></div>
          <div><small>年龄: <span>{{uAge}}</span></small></div>
      </div>
  `,
  data: function () {
      return {
          uName: 'Walter',
          uAge: 19,
      }
  }
});

var demo = new Vue({
  el:"#demo"
});
```
> `一般都是使用这个东西 Vue.component 建议`


##### 3.自定义标签名称的问腿
`因为 Vue 只有在浏览器解析和标准化 HTML 后才能获取模版内容。尤其像这些元素 <ul> ， <ol>， <table> ， <select> 限制了能被它包裹的元素， <option> 只能出现在其它元素内部。在自定义组件中使用这些受限制的元素时会导致一些问题，例如：`

`不要使用HTML内部的标签名称作为 自定义标签名称`
```html
<table>
<my-row>...</my-row>
</table>
```
`自定义组件 <my-row> 被认为是无效的内容，因此在渲染的时候会导致错误。变通的方案是使用特殊的 is 属性：`
```html
<table>
<tr is="my-row"></tr>
</table>
```

##### 4.data 必须是函数
`为啥 因为组件要实现复用 总不能让多个这个组件的实例都引用同一个数据吧！`


##### 5.组件的分类
* 局部组件

  ```javascript
  var Child = {
  template: '<div>A custom component!</div>'
  }
  new Vue({
  // ...
  components: {
      // <my-component> 将只在父模板可用
      'my-component': Child
  }
  ```

* 全局组件

  ```javascript
  Vue.component('my-component', {
  template: '<div>A custom component!</div>'
  })

  ```

##### 6.组件的数据[简单]
* 1.通过data 存储数据

  ```javascript
  Vue.component("key-value", {
      template:`
          <div class="pair">
              <small class="key">{{key}}</small> : <small class="key">{{value}}</small>
          </div>
      `,
      data:function(){
          return {
              key:"Name",
              value:"王小明"
          }
      }
  });
  ```

##### 7.动态组件
`多个组件可以使用同一个挂载点，然后动态地在它们之间切换。使用保留的 <component> 元素，动态地绑定到它的 is 特性：`

例子: `dynamicComponent.html`
```javascript
<div id="demo">
  <p v-cloak>学号:{{id}}</p>
  <button @click="handler($event)" >点击切换</button>
  <component :is="showLable"></component>
</div>

var demo = new Vue({
  el: "#demo",
  data: {
      id: "2016110418",
      showLable:"user-label-lzm"
  },
  methods: {
      handler(e){
          this.showLable = this.showLable == 'user-label-lzm'? "user-label-ljk":"user-label-lzm";
      }
  },
  components: {
      'user-label-lzm': {
          template: `            
              <div>
                  <div><small>姓名: <span>{{uName}}</span></small></div>
                  <div><small>年龄: <span>{{uAge}}</span></small></div>
              </div>`,
          data: function () {
              return {
                  uName: '李志民',
                  uAge: 20,
              }
          }
      },
      'user-label-ljk':{
          template: `            
              <div>
                  <div><small>姓名: <span>{{uName}}</span></small></div>
                  <div><small>年龄: <span>{{uAge}}</span></small></div>
              </div>`,
          data: function () {
              return {
                  uName: '李嘉坤',
                  uAge: 25,
              }
          }
      }
  }
});

```

##### 8.keep-alive 组件
`<keep-alive> 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 <transition> 相似，<keep-alive>
是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。
当组件在 <keep-alive> 内被切换，它的 activated 和 deactivated 这两个生命周期钩子函数将会被对应执行。
主要用于保留组件状态或避免重新渲染。`



##### 9.组件之间的关系
* `1.组件之间可以再嵌套组件`
  * `但是子组件只能在父组件内部使用解析` 
* `2.子组件无法访问父组件中数组每个组件的作用域是互相独立的`

`例子`:`fatherSonComponent.html`
```javascript
var demo = new Vue({
  el: "#demo",
  data: {
      id: "2016110418",
      showLable:"user-label"
  },
  methods: {
      handler(e){
          this.showLable = this.showLable == 'user-label-lzm'? "user-label-ljk":"user-label-lzm";
      }
  },
  components: {
      'user-label': {
          template: `            
              <div>
                  <div><small>姓名: <span>{{uName}}</span></small></div>
                  <div><small>年龄: <span>{{uAge}}</span></small></div>
                  <label-grade></label-grade>
              </div>`,
          data: function () {
              return {
                  uName: '李志民',
                  uAge: 20,
              }
          },
          components:{
              'label-grade':{
                  template: `            
                      <div>
                          <div><small>数学: <span>{{math}}</span></small></div>
                          <div><small>英语: <span>{{englist}}</span></small></div>
                      </div>`,
                  data: function () {
                      return {
                          math: 89.5,
                          englist: 99,
                      }
                  }
              }
          }
      }
  }
});

```

##### 10.组件之间数据传递
1.`组件实例的作用域是孤立的。这意味着不能并且不应该在子组件的模板内直接引用父组件的数据。可以使用 props 把数据传给子组件。`

2.`prop 是父组件用来传递数据的一个自定义属性。子组件需要显式地用 props 选项 声明 “prop”：`

3.`说明: prop 类似一个接口 子组件可以觉得要接受什么数据 然后父组件可以传递什么数组`

4.`props 类型： 字符串数组/对象 规定里面写的都是单个单词 并且单词全小写`

```html
<body>
  <div id="demo">
      <p v-cloak>学号:{{id}}</p>
      <user-detail v-for="item in users" :key="item.id" :name="item.name"  :age="item.age" :id="item.id" ></user-detail>
  </div>
  <template id="com-userDetail">
      <div>
          <hr/>
          <div><small>学号: <span>{{id}}</span></small></div>
          <div><small>姓名: <span>{{name}}</span></small></div>
          <div><small>年龄: <span>{{age}}</span></small></div>
      </div>
  </template>
</body>
<script>
  var demo = new Vue({
      el: "#demo",
      data: {
          id: "2016110418",
          showLable:"user-label",
          users:[
              {
                  id:"2016110418",
                  name:"蒋星",
                  age:18
              },
              {
                  id:"2016110419",
                  name:"蒋星",
                  age:18
              }
          ]
      },
      components: {
          'user-detail': {
              props:['name','age','id'],
              template: "#com-userDetail",
          }
      }
  });
</script>
```
##### 11. props 里面的配置约定 
`设计来干嘛呀？ 用于写组件库用。公开的组件 告诉别人传递约定的参数`

```javascript
Vue.component('props-demo-advanced', {
props: {
  // 只检测类型
  height: Number,
  // 检测类型 + 其他验证
  age: {
    type: Number,
    default: 0,
    required: true,
    validator: function (value) {
      return value >= 0
    }
  }
}
})
```

* `type 可选的类型`
  * `String`
  * `Number`
  * `Boolean`
  * `Function`
  * `Object`
  * `Array`
  * `Symbol`
* `required 必须传递`
* `default 默认值`
* `validator 验证规则`


##### 12. 组件中的数据的形式
1.data

2.props 

3.computed 计算属性

##### 13.父组件访问子组件的数据
`我们知道，父组件是使用 props 传递数据给子组件，但如果子组件要把数据传递回去，应该怎样做？那就是自定义事件！ $emit(事件名称,数据) $on`

----

`Vue的事件系统分离自浏览器的EventTarget API。尽管它们的运行类似，但是$on 和 $emit 不是addEventListener 和 dispatchEvent 的别名。`

----
* 1.使用 $on(eventName) 监听事件

* 2.在子组件中使用 vm.$emit('事件名称','数据') 触发一个自定义事件 发送数据;
  * `父组件通过v-on 监听子组件自定义事件`

```javascript
<body>
  <div id="counter-event-example">
      <p>{{ total }}</p>
      <button-counter v-on:increment="incrementTotal"></button-counter>
      <button-counter v-on:increment="incrementTotal"></button-counter>
  </div>
</body>
<script>
  Vue.component('button-counter', {
      template: '<button v-on:click="increment">{{ counter }}</button>',
      data: function () {
          return {
              counter: 0
          }
      },
      methods: {
          increment: function () {
              let size = 2;
              this.counter += size;
              this.$emit('increment',size); //后面参数 [...] 类型
          }
      },
  })
  new Vue({
      el: '#counter-event-example',
      data: {
          total: 0
      },
      methods: {
          incrementTotal: function (size) {
              this.total += size;
          }
      }
  })
</script>
```

##### 14.监视组件的原始事件

`有时候，你可能想在某个组件的根元素上监听一个原生事件。可以使用 .native 修饰 v-on 。例如：`

```html
<my-component v-on:click.native="doTheThing"></my-component>
```

##### 15.单向数据流
* `prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来。这是为了防止子组件无意修改了父组件的状态——这会让应用的数据流难以理解。每次父组件更新时，子组件的所有 prop 都会更新为最新值。这意味着你不应该在子组件内部改变 prop 。如果你这么做了，Vue 会在控制台给出警告。`
* `注意在 JavaScript 中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。`

* `通常有两种改变 prop 的情况：`
  * `prop 作为初始值传入，子组件之后只是将它的初始值作为本地数据的初始值使用；给本地变量赋值`

```javascript
props: ['initialCounter'],
    data: function () {
    return { counter: this.initialCounter }
}
```
* `prop 作为需要被转变的原始值传入。`
```javascript
props: ['size'],
computed: {
    normalizedSize: function () {
        return this.size.trim().toLowerCase()
    }
}
```
* `如果子组件想修改数据并且同步更新到父组件中,两个方法`
* `使用aync 关键字 但是你需要显示的触发一个事件 change 联合 $emit使用`
`本质上来讲其实就是利用 $emit 来修改数据值 不使用aync 关键字都可以完成任务`

```html
 <body>
    <template id="input-name">
        <div>
            姓名: <input type="text" v-model:value="itemName"  >
            <button @click="change">修改数据</button>
        </div>
    </template>    

    <div id="demo2">
        <div>
            <small>姓名: <b >{{name}}</b> </small>
            <name-input :name.aync='name' @update:name="val => name = val"></name-input>
        </div>
    </div>
</body>
<script>    
    new Vue({
        el:"#demo2",
        data:{
            name:"jxKicker"
        },
        components:{
            'name-input':{
                props:['name'],
                data(){
                    return {
                        itemName:this.name
                    }
                },
                template:"#input-name",
                methods:{
                    change(){
                        this.$emit('update:name',this.itemName);
                    }
                }
            }
        }
    });
</script>
```


##### 16.非父子组件的通信

* 1.通过一个空的vue实例作为中央事件中心 里就是利用 API: $on 侦听事件 $obj.$emit() 和组件生命周期
    * `1. Event.$emit(事件名称,数据);`
    * `2. Event.$on(事件名称,data => { });`:`注:一定要是箭头函数 不然this 指向 Event 而不是接受数据的vue 实例`

```javascript
 var Event = new Vue();

 var A = vue({
     ...
     methods:{
         send(){
             Event.$emit('send-name-to-B','this is my Data');
         }
     }
 });

 var B = vue({
     ...
     data:{
         message = ""
     },
     ...
     mounted(){
         Event.$on('send-name-to-B',data => {
             this.message = data;
         })
     }
 })
```

##### 17. slot 内容分发
`作用: 获取组件中的原内容`

1. 单个slot  `处理组件中的html 元素`

```javascript
<body>
    <div id="demo">
        <p v-cloak>学号:{{id}}</p>
        <user-label>
            <ul>
                <li>1. 学号 2016110418</li>
                <li>2. 学号 2016110419</li>
                <li>3. 学号 2016110420</li>
                <li>4. 学号 2016110421</li>
                <li>5. 学号 2016110422</li>
            </ul>
        </user-label>
    </div>
</body>
<script>
    var demo = new Vue({
        el: "#demo",
        data: {
            id: "2016110418",
            showLable:"user-label"
        },
        components: {
            'user-label': {
                template: `
                <div>
                    <div><small>姓名: <span>{{uName}}</span></small></div>
                    <div><small>年龄: <span>{{uAge}}</span></small></div>
                    <slot></slot>
                </div>
                `,
                data: function () {
                    return {
                        uName: '李志民',
                        uAge: 20,
                    }
                }
            }
        }
    });
</script>
```

2. 具名组件 利用 slot 属性指定名称 

```javascript
<div id="demo">
    <p v-cloak>学号:{{id}}</p>
    <user-label>
        <ol slot="id">
            <li>学号 2016110418</li>
            <li>学号 2016110419</li>
            <li>学号 2016110420</li>
            <li>学号 2016110421</li>
            <li>学号 2016110422</li>
        </ol>

        <div slot="detail">
            <small>五个学生 的个人信息简介</small>
        </div>
    </user-label>
</div>
var demo = new Vue({
    el: "#demo",
    data: {
        id: "2016110418",
        showLable:"user-label"
    },
    components: {
        'user-label': {
            template: `
            <div>
                <slot name="detail"></slot>
                <div><small>姓名: <span>{{uName}}</span></small></div>
                <div><small>年龄: <span>{{uAge}}</span></small></div>
                <slot name="id"></slot>
            </div>
            `,
            data: function () {
                return {
                    uName: '李志民',
                    uAge: 20,
                }
            }
        }
    }
});
```


