[条件渲染 Vue ](#top) <b id="top"></b>  :maple_leaf:
----
`条件渲染涉及到几个指令` `v-if` `v-else` `v-else-if` `v-show` `再解决一些复用问题就可以了`

##### [if 指令家族](#top)
```html
<div id="val">
    <p  v-show="isVip" v-bind:class="Vipclass"  > <small>{{name}}先生 你是尊贵的Vip 会员</small>
        <span v-if="VipDegree == 1"> <label class=" label-danger label"> Vip 1 高级会员</label> </span>
        <span v-else-if="VipDegree == 2"> <label class=" label-danger label"> Vip 2 超级会员</label> </span>
        <span v-else> <label class=" label-danger label"> Vip 3 钻石会员</label> </span>       
    </p>
    <label v-if="sex"  class=" label label-primary">男生</label>
    <label v-else  class=" label label-primary">女生</label>
</div>
```
[vue 代码](#top)
```node
let person = new Vue({
    el:"#val",
    data:{
        isVip:true,
        VipDegree:3,
        Vipclass:"text-muted",
        name:"JiangXing",
        age:18,
        sex:true
    }
});
```
![结果图](/Resources/vue/v-if.png)

##### [用 key 管理可复用的元素](#top)
* `Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。这么做除了使 Vue 变得非常快之外，还有其它一些好处。
例如，如果你允许用户在不同的登录方式之间切换：`
* `这样也不总是符合实际需求，所以 Vue 为你提供了一种方式来表达“这两个元素是完全独立的，不要复用它们”。只需添加一个具有唯一值的 key 属性即可：`
```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```
