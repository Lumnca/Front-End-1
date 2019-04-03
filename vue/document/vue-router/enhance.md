#### [vue-router 使用它](#top) <b id="top"></b>
----
`来吧我们来开始它`

##### 1.如果你想要通过代码改变路由
```node
const userId = '123'

this.$router.push({ name: 'user', params: { userId }}) // -> /user/123  user 的意思是路由的名称
this.$router.push({ path: `/user/${userId}` }) // -> /user/123
// 这里的 params 不生效
this.$router.push({ path: '/user', params: { userId }}) // -> /user
```
