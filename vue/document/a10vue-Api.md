### [vue.js 全局 API](#top) <b id="top"></b>
`vue.js 全局指令`:white_check_mark:

------

- [x] [`1.自定义指令`](#target1)
- [x] [`2.title2`](#target2)
- [x] [`3.title3`](#target3)

------

#####  [1.自定义指令 Vue.directive( id, [definition])](#top) <b id="target1"></b> 
`概括`：`我们可以在vue中自定义指令按照vue给出了约定`
* `自定义全局指令 注: 自定义指令使用的时候需要加上 v- 前缀`

```node
// 注册
Vue.directive('hello', {
  bind: function (el,binding) {
    console.log('当指令绑定到元素上的时候调用，只调用一次,可执行初始化操作');
  },
  inserted: function (el,binding) {
    console.log('当被绑定元素插入到dom树中');
  },
  update: function (el,binding) {
    console.log('当被绑定元素插入所在模板更新的时候');
  },
  componentUpdated: function () {
    console.log('被绑定元素所在模板完成一次周期调用');
  },
  unbind: function () {
    console.log('指令和元素解绑的时候');
  }
})

// 注册 (指令函数)
Vue.directive('hello', function () {
  // 这里将会被 `bind` 和 `update` 调用 因为他们两个是最常用的其他的三个钩子函数我们很少用
})

// getter，返回已注册的指令
var hello = Vue.directive('hello')
```

```html
 <div id="directive">
    <h3 v-hello="description">自定义属性</h3>
 </div>
 <!-- description 是一个变量 --> 
```


`钩子函数的参数`

```node
指令钩子函数会被传入以下参数：
el：指令所绑定的元素，可以用来直接操作 DOM 。

binding：一个对象，包含以下属性：

    name：指令名，不包括 v- 前缀。

    value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。

    oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。

    expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。

    arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。

    modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。

```

###### [定义局部指令](#top)
`如果想注册局部指令，组件中也接受一个 directives 的选项：例如定义一个 focus 焦点`

```node
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```
#####  [2.title2](#top) <b id="target2"></b> 
`概括`


#####  [3.title3](#top) <b id="target3"></b> 
`概括`




--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `任意使用` 
