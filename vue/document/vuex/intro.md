#### [:octocat: vuex 状态管理器](#top) <b id="top"></b>

----
`用于多组件之间的数据共享,为啥要这样呢？ 因为我们是单页面应用啊! 对就是这样！Vuex 是一个专为 Vue.js 应用程序
开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。`

- [x] [`1.开始使用它`](#target1)



----
###### [1.开始使用它](#top) <b id="target1"></b>
`让我们先建立一个小的demo 项目`
```shell
vue init webpack-simple vuex-demo

cd vuex-demo

npm install

npm install vuex -D
```
`或者这样一下全部安装`

```shell
vue init webpack vuex-demo

cd vuex-demo

npm install
```

`每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态
(state)。Vuex 和单纯的全局对象有以下两点不同：`

##### [2.store.js](#top)
`定义state 每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和
单纯的全局对象有以下两点不同：`
* `1.Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。`
* `2.你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态
的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。`

`请注意在js vuex管理文件头部加上这个`
```node
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

```
##### [3.State](#top)
`Vuex 使用单一状态树——是的，用一个对象就包含了全部的应用层级状态。至此它便作为一个“唯一数据源 (SSOT)”而存在。
这也意味着，每个应用将仅仅包含一个 store 实例。单一状态树让我们能够直接地定位任一特定的状态片段，在调试的过程
中也能轻易地取得整个当前应用状态的快照`
`store.js`
```node
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 6
  }
})

export default store

```


###### [在 Vue 组件中获得 Vuex 状态](#top)
`从 store 实例中读取状态最简单的方法就是在计算属性中返回某个状态：`

```node
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return store.state.count
    }
  }
}
```

`Vuex 通过 store 选项，提供了一种机制将状态从根组件“注入”到每一个子组件中（需调用 Vue.use(Vuex)）：`
```node
const app = new Vue({
  el: '#app',
  // 把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件
  store,
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```

`通过在根实例中注册 store 选项，该 store 实例会注入到根组件下的所有子组件中，且子组件能通过 this.$store 访问到。让我们更新下 Counter 的实现：`

```node
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}
```

###### [mapState 辅助函数](#top)
`当一个组件需要获取多个状态时候，将这些状态都声明为计算属性会有些重复和冗余。为了解决这个问题，我们可以
使用 mapState 辅助函数帮助我们生成计算属性，让你少敲代码：`

```node
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```
`当映射的计算属性的名称与 state 的子节点名称相同时，我们也可以给 mapState 传一个字符串数组。`

```node
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```

`所以在组件中还可以写成这样`
```node
import { mapState } from 'vuex'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '李志明是我的儿子'
    }
  },
  computed: mapState([ 'count', 'userName' ])
}
```

```
使用 Vuex 并不意味着你需要将所有的状态放入 Vuex。虽然将所有的状态放到 Vuex 会使状态变化更显式和易调试，但

也会使代码变得冗长和不直观。如果有些状态严格属于单个组件，最好还是作为组件的局部状态。你应该根据你的应用开

发需要进行权衡和确定。
```

##### [4.Getter](#top)
`有时候我们需要从 store 中的 state 中派生出一些状态，例如对列表进行过滤并计数：类似于面向对象语言中的字段对应的属性 原则上规定能获得state的途径
只能是一个地方 getter 而不是在直接通过 state 获取`

`store.js`
```node
import Vuex from 'vuex'
import Vue from 'vue'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 6,
    userName: '打王者',
    age: 18,
    sex: true
  },
  getters: {
    info: state => {
      return `name:${state.userName} age:${state.age} sex:${state.sex ? '男' : '女'}`
    }
  }
})

export default store
```

```node
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```
`Getter 会暴露为 store.getters 对象，你可以以属性的形式访问这些值：`
```node
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '李志明是我的儿子'
    }
  },
  computed: {
    info () {
      //要加上this
      return this.$store.getters.info
    }
  }
}
```
###### [通过方法访问](#top)

```node
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}

this.$store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```

###### [mapGetters 辅助函数](#top)
`mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性：`
```node
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
  // 使用对象展开运算符将 getter 混入 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```
`如果你想将一个 getter 属性另取一个名字，使用对象形式：`
```node
mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
```
