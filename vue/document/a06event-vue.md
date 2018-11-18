### [vue 事件处理](#top) :maple_leaf: <b id="top"></b> 

----
`vue 对事件处理提供了许多的方法,简化时间操作`

- [x] :maple_leaf: [监听事件](#exmaple)
- [x] :maple_leaf: [事件处理方法](#exmaple)


#### [监听事件](#top) :maple_leaf:  <b id="exmaple"></b>  
可以用 v-on 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码

```html
<div id="example-1">
  <button v-on:click="counter += 1">Add 1</button>
  <p>The button above has been clicked {{ counter }} times.</p>
</div>
```
Vue 实例
```node
var example1 = new Vue({
  el: '#example-1',
  data: {
    counter: 0
  }
})
```

#### [事件处理方法](#top) :maple_leaf:  <b id="exmaple"></b>  
(1) 有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 $event 把它传入方法： 使用 `v-on` 指定监听某种事件类型 可以传递 `$event` 参数指定事件对象 <br/> <br/>
(2) 时间处理函数 可以传递 `$event`参数 处理方法可以写在methods 对象中 <br/>
```html
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet($event)">Greet</button>
</div>
```
```node
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'
```

##### 参数问题
```html
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
  <button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
  </button>
</div>
```
vue 代码
```node
new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    },
    warn: function (message, event) {
      // 现在我们可以访问原生事件对象
      if (event) event.preventDefault()
    alert(message)
  }
    
  }
})
```
