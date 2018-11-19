### [vue 事件处理](#top) :maple_leaf: <b id="top"></b> 

----
`vue 对事件处理提供了许多的方法,简化事件操作`

- [x] :maple_leaf: [监听事件](#exmaple)
- [x] :maple_leaf: [事件处理方法](#handler)
- [x] :maple_leaf: [事件修饰符](#desc)
- [x] :maple_leaf: [按键修饰符](#key)
- [x] :maple_leaf: [系统修饰键](#system)


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

#### [事件处理方法](#top) :maple_leaf:  <b id="handler"></b>  
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
  <button @click="handler(sex, $event)" class="btn btn-sm btn-primary">点击我吧</button>
</div>
```
vue 代码
```node
new Vue({
  el: '#example-3',
  data:{
     sex:true
  },
  methods: {
    say: function (message) {
      alert(message)
    },
    warn: function (message, event) {
      // 现在我们可以访问原生事件对象
      if (event) event.preventDefault()
      alert(message)
    },  
    handler:function(sex,event){
        console.log(sex);
        console.log(event);
    }
 }
});
```
#### [事件修饰符](#top) :maple_leaf:  <b id="desc"></b>  
`在事件处理程序中调用 event.preventDefault() 或 event.stopPropagation() 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。为了解决这个问题，Vue.js 为 v-on 提供了事件修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。`
* .stop
* .prevent
* .capture
* .self
* .once
* .passive

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>

<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>

<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```
(1) 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。 <br/>

(2) 不要把 .passive 和 .prevent 一起使用，因为 .prevent 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，.passive 会告诉浏览器你不想阻止事件的默认行为。
#### [按键修饰符](#top) :maple_leaf:  <b id="key"></b>
`在监听键盘事件时，我们经常需要检查常见的键值。Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：`

```html
<!-- 只有在 `keyCode` 是 13 时调用 `vm.submit()` -->
<input v-on:keyup.13="submit">
```
(1). 记住所有的 keyCode 比较困难，所以 Vue 为最常用的按键提供了别名：<br/>
```html
<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
```
* .enter
* .tab
* .delete (捕获“删除”和“退格”键)
* .esc
* .space
* .up
* .down
* .left
* .right

(2).可以通过全局 config.keyCodes 对象自定义按键修饰符别名：<br/>
```node
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```
#### [系统修饰键](#top) :maple_leaf:  <b id="system"></b>
`可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。`
* .ctrl
* .alt
* .shift
* .meta
> 注意：在 Mac 系统键盘上，meta 对应 command 键 (⌘)。在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。
<Br/>

```html
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

##### .exact 修饰符
`.exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。`

```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

##### 鼠标按钮修饰符
`这些修饰符会限制处理函数仅响应特定的鼠标按钮。`
* .left
* .right
* .middle
<br/>

(1). 当一个 ViewModel 被销毁时，所有的事件处理器都会自动被删除。你无须担心如何清理它们。 <br/>





































