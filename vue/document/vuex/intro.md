#### [:octocat: vuex 状态管理器](#top) <b id="top"></b>

----
`用于多组件之间的数据共享,为啥要这样呢？ 因为我们是单页面应用啊! 对就是这样！Vuex 是一个专为 Vue.js 应用程序
开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。`

- [x] [`1.开始使用它`](#target1)
- [x] [`2.store.js`](#target2)
- [x] [`3.State`](#target3)
- [x] [`4.Getter`](#target4)
- [x] [`5.Action`](#target5)
- [x] [`6.Mutation`](#target6)

----
##### [核心的图片](#top)

![核心图片](https://vuex.vuejs.org/vuex.png)


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

##### [2.store.js](#top)  <b id="target2"></b>
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
##### [3.State](#top)  <b id="target3"></b>
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

##### [4.Getter](#top) <b id="target4"></b>
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

##### [5.Action](#top) <b id="target5"></b>
`Action 类似于 mutation，不同在于：Action 提交的是 mutation，而不是直接变更状态。Action 可以包含任意异步操作。 `  `他就像一个事件一样
激发一个事件,并且充当一个过滤数据的中间管道 然后将真正的处理过程交给 mutation`

```node
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```
`Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 context.commit 提交一个 mutation，
或者通过 context.state 和 context.getters 来获取 state 和 getters。当我们在之后介绍到 Modules 时，你就知道 context
对象为什么不是 store 实例本身了。`

```node
mutations: {
  increment (state) {
    state.count += 2
  },
  AddAny (state, params) {
    console.log(params)
    state.count += params.number
  }
},
actions: {
  increment (context) {
    context.commit('increment')
  },
  AddNumher (context, params) {
    if (params.number < 0) {
      console.error('val:', '传递了非法的参数,参数应该为 大于0的')
    } else {
      context.commit('AddAny', params)
    }
  }
}
```
`你不能直接调用一个 mutation handler。这个选项更像是事件注册：“当触发一个类型为 increment 的 mutation 时，调用此函数。”要唤醒一个 mutation handler，你需要以相应的 type 调用 store.commit 方法：`
```node
store.commit('increment')
```

----
`Action 通过 store.dispatch 方法触发：`
```node
methods: {
  Add () {
    this.$store.dispatch('increment')
  },
  sendParameter () {
    this.$store.dispatch('AddNumher', { number: 18 })
  }
}
```
----
`Actions 支持同样的载荷方式和对象方式进行分发：`

```node
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

`在组件中分发 Action`

```node
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

##### [6.Mutation](#top) <b id="target6"></b>
`更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数：`

```node
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
```
`你不能直接调用一个 mutation handler。这个选项更像是事件注册：“当触发一个类型为 increment 的 mutation 时，调用此函数。”要唤醒一个 mutation handler，你需要以相应的 type 调用 store.commit 方法：`
```node
store.commit('increment')
```

##### Mutation 需遵守 Vue 的响应规则
`既然 Vuex 的 store 中的状态是响应式的，那么当我们变更状态时，监视状态的 Vue 组件也会自动更新。这也意味着 Vuex 中的 mutation 也需要与使用 Vue 一样遵守一些注意事项：`

* `最好提前在你的 store 中初始化好所有所需属性。`

* `当需要在对象上添加新属性时，你应该`

* `使用 Vue.set(obj, 'newProp', 123), 或者`

* `以新对象替换老对象。例如，利用 stage-3 的对象展开运算符我们可以这样写：`
```node
state.obj = { ...state.obj, newProp: 123 }
```

##### 使用常量替代 Mutation 事件类型
`使用常量替代 mutation 事件类型在各种 Flux 实现中是很常见的模式。这样可以使 linter 之类的工具发挥作用，同时把这些常量放在单独的文件中可以让你的代码合作者对整个 app 包含的 mutation 一目了然：`

```node
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

##### Mutation 必须是同步函数
`一条重要的原则就是要记住 mutation 必须是同步函数。为什么？请参考下面的例子：`

```node
mutations: {
  someMutation (state) {
    api.callAsyncMethod(() => {
      state.count++
    })
  }
}
```
##### 在组件中提交 Mutation
`最好不要这样做 你可以在组件中使用 this.$store.commit('xxx') 提交 mutation，或者使用 mapMutations 辅助函数将组件中的 methods 映射为 store.commit 调用（需要在根节点注入 store）。`

```node
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}

```

##### 最后的 store文件
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
    },
    studentCount: state => {
      return `count: ${state.count}`
    }
  },
  mutations: {
    increment (state) {
      state.count += 2
    },
    AddAny (state, params) {
      console.log(params)
      state.count += params.number
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    },
    AddNumher (context, params) {
      if (params.number < 0) {
        console.error('val:', '传递了非法的参数,参数应该为 大于0的')
      } else {
        context.commit('AddAny', params)
      }
    }
  }
})

export default store

```
