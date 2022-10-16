# 什么是Pinia?
- 用起来像组合式API(Composition API)
- 兼容Vue2、Vue3
- 状态管理的库，用于跨组件、页面进行状态共享(这点和Vuex、Redux一样)
#  和Vuex相比，Pinia有很多的优势:
- mutations 不再存在:
- 更友好的TypeScript支持
- 不再有modules的嵌套结构:
✓ 你可以灵活使用每一个store，它们是通过扁平化的方式来相互使用的;
- 也不再有命名空间的概念，不需要记住它们的复杂关系;
# Store有三个核心概念:
- state、getters、actions;
- 等同于组件的data、computed、methods;
- 一旦 store 被实例化，你就可以直接在 store 上访问 state、getters 和 actions 中定义的任何属性;
# 如何使用Pinia?
## 安装
```
yarn add pinia
``` 

## 创建一个pinia并且将其传递给应用程序:index.js
```
import {createPinia} from 'pinia'
const pinia = createPinia()
export default pinia
```
main.js引入pinia
```
import pinia from './stores'
createApp(App).use(pinia).mount('#app')
```
## 定义 
### Store:
- 引用 defineStore() 定义
- 一个唯一名称，作为第一个参数传递  
### 定义 Getters:
1. Getters相当于Store的computed:
- 用 defineStore() 中的 getters 属性定义
- getters中可以定义接受一个state作为参数的函数
- 可以通过this访问整个store实例的所有操作
### 定义Actions
- 在action中可以通过this访问整个store实例的所有操作
- Actions中是支持异步操作
home.vue //Actions中是支持异步操作例子
```
 const homeStore = useHome()
  homeStore.fetchHomeMultidata().then(res => {
    console.log("fetchHomeMultidata的action已经完成了:", res)
  })
```

```
import { defineStore } from 'pinia'
const useHome = defineStore("home", {
  state: () => ({
    banners: [],
    recommends: []
  }),
  actions: {
    async fetchHomeMultidata() {
      const res = await fetch("http://123.207.32.32:8000/home/multidata")
      const data = await res.json()

      this.banners = data.data.banner.list
      this.recommends = data.data.recommend.list
    }
  }
})

export default useHome
```

counter.js

```
// 定义关于counter的store
import { defineStore } from 'pinia'

import useUser from './user'

const useCounter = defineStore("counter", {
  state: () => ({
    count: 99,
    friends: [
      { id: 111, name: "why" },
      { id: 112, name: "kobe" },
      { id: 113, name: "james" },
    ]
  }),
  getters: {
    // 1.基本使用
    doubleCount(state) {
      return state.count * 2
    },
    // 2.一个getter引入另外一个getter
    doubleCountAddOne() {
      // this是store实例
      return this.doubleCount + 1
    },
    // 3.getters也支持返回一个函数
    getFriendById(state) {
      return function(id) {
        for (let i = 0; i < state.friends.length; i++) {
          const friend = state.friends[i]
          if (friend.id === id) {
            return friend
          }
        }
      }
    },
    // 4.getters中用到别的store中的数据
    showMessage(state) {
      // 1.获取user信息
      const userStore = useUser()

      // 2.获取自己的信息

      // 3.拼接信息
      return `name:${userStore.name}-count:${state.count}`
    }
  },
  actions: {
    increment() {
      this.count++
    },
    incrementNum(num) {
      this.count += num
    }
  }
})

export default useCounter

```

## 使用定义的Store
- Store在它被使用之前是不会创建的，我们可以通过调用use函数来使用Store:


```
<template>
  <div class="home">
        <h2>{{counterStore.counter}}</h2>
  </div>
</template>

<script setup>
import useCounter from '@/stores/counter'
const counterStore = useCounter()
</script>
```

- 解构Store会失去响应式:需要使用storeToRefs()或Vue原生toRefs()
- 

```
const {counter} = counterStore //不是响应式
const {counter: counter1} = toRefs(counterStore) //Vue原生toRefs()
const {counter: counter2} = storeToRefs() //Pinia自带(counterStore)
```

###  操作State: .vue组建中
1. 读取和写入 state:  默认情况下，可以通过 store 实例访问状态来直接读取和写入状态;

```
const counterStore = useCounter()
counterStore.counter++
```
2.重置 State: 可以通过调用 store 上的 $reset() 方法将状态重置到其初始值;
```
const counterStore = useCounter()
 function resetState() {
    userStore.$reset()
  }
```
3. 调用 $patch 方法同时应用多个更改
```
const counterStore = useCounter()
counterStore.$patch = {
    counter: 1,
    name: 'qq'
}
```
4. $state 新对象来替换 Store 的整个状态
```
counterStore.$state = {
    counter: 1,
    name: 'qq'
}
```
### 访问Getters

```
<template>
  <div class="home">
    <h2>Home View</h2>
    <h2>doubleCount: {{ counterStore.doubleCount }}</h2>
    <h2>doubleCountAddOne: {{ counterStore.doubleCountAddOne }}</h2>
    <h2>friend-111: {{ counterStore.getFriendById(111) }}</h2>
    <h2>friend-112: {{ counterStore.getFriendById(112) }}</h2>
    <h2>showMessage: {{ counterStore.showMessage }}</h2>
    <button @click="changeState">修改state</button>
    <button @click="resetState">重置state</button>
  </div>
</template>

<script setup>
  import useCounter from '@/stores/counter';

  const counterStore = useCounter()

</script>
```
