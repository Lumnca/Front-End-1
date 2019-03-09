### [vue 动画](#top) <b id="top"></b>
---
`Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加 entering/leaving 过渡`

------

- [x] [`1.例子`](#target1)
- [x] [`2.四个类名的解释`](#target2)
- [x] [`3.title3`](#target3)

------

#####  [1.例子](#top) <b id="target1"></b> 
`元素封装成过渡组件之后，在遇到插入或删除时，Vue 将`
   * `自动嗅探目标元素是否有 CSS 过渡或动画，并在合适时添加/删除 CSS 类名。`
   * `如果过渡组件设置了过渡的 JavaScript 钩子函数，会在相应的阶段调用钩子函数。`
   * `如果没有找到 JavaScript 钩子并且也没有检测到 CSS 过渡/动画，DOM 操作（插入/删除）在
   下一帧中立即执行。(注意：此指浏览器逐帧动画机制，与 Vue，和Vue的 nextTick 概念不同`
   
```html
<div id="demo">
  <button v-on:click="show = !show">
    Toggle
  </button>
  <transition name="fade">
    <p v-if="show">hello</p>
  </transition>
</div>

new Vue({
  el: '#demo',
  data: {
    show: true
  }
})

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}
<style>
```



#####  [2.四个类名的解释](#top) <b id="target2"></b> 

```node
会有 4 个(CSS)类名在 enter/leave 的过渡中切换

  v-enter: Dom要显示出来了 给这个Dom 加上这个样式

  v-enter-active: Dom 出场的动画 完成出场后删除这些样式

  v-leave: Dom 将要离开了 此时给Dom 加上这个类 

  v-leave-active: 定义离开过程总的动画 离开完成后 Dom 被移出

```

#####  [3.title3](#top) <b id="target3"></b> 
`概括`




--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `任意使用` 
