### [vue 动画](#top) <b id="top"></b>
---
`Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加 entering/leaving 过渡`

------

- [x] [`1.例子`](#target1)
- [x] [`2.四个类名的解释`](#target2)
- [x] [`3.自定义类名`](#target3)

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
        <h4 v-if="show" class="">My Name is What!</h4>
    </transition>
</div>

new Vue({
  el: '#demo',
  data: {
    show: true
  }
})

<style>
.fade-enter-active{
    /* 进行动画配置 */
    transition: all 0.5s;
}

.fade-enter{
    /* 定义进入的过渡动画 */
    line-height: 50px;
    padding: 5px;
    padding-left: 50px;
    border-radius: 10px;
}


.fade-leave-active {
    /* 定义离开的动画 */
    padding-left: 50px; 
    transition: all 0.5s;
    transition-timing-function: linear;
}
<style>
```
`所以 css类其实可以这样写`
```css
.fade-enter-active {
  animation: bounce-in .5s;
}

.fade-leave-active {
  animation: bounce-out .5s;
}

@keyframes bounce-in {
  0% {
      transform: scale(0);
  }

  50% {
      transform: scale(1.5);
  }

  100% {
      transform: scale(1);
  }
}

@keyframes bounce-out {
  0% {
      transform: scale(1);
  }

  50% {
      transform: scale(1.5);
  }

  100% {
      transform: scale(0);
  }
}
```

#####  [2.四个类名的解释](#top) <b id="target2"></b> 

```node
会有 4 个(CSS)类名在 enter/leave 的过渡中切换

  v-enter: Dom要显示出来了 给这个Dom 加上这个样式

  v-enter-active: Dom 出场的动画 完成出场后删除这些样式

  v-leave: Dom 将要离开了 此时给Dom 加上这个类 

  v-leave-active: 定义离开过程总的动画 离开完成后 Dom 被移出

```

#####  [3.自定义类名](#top) <b id="target3"></b> 
`概括:我们可以通过以下特性来自定义过渡类名：`
* `enter-class`
* `enter-active-class`
* `leave-class`
* `leave-active-class`

```html
<link href="https://cdn.bootcss.com/animate.css/3.7.0/animate.css" rel="stylesheet">

<div id="example-3">
    <button @click="show = !show">
        Toggle render
    </button>
    <transition enter-active-class="animated bounceInLeft" leave-active-class="animated bounceOutRight">
        <p v-if="show" >hello</p>
    </transition>
</div>
```


--------------------
`作者:` `模板` 
`完成时间`:`2018年12月31日18:33:38`
`备注信息`: `任意使用` 
