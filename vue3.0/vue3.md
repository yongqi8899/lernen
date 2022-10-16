# 什么是Vue？ 
 - 是一套用于构建用户界面的渐进式框架 
 - Vue的本质，就是一个JavaScript的库 
 - 什么是渐进式框架呢?表示我们可以在项目中一点点来引入和使用Vue，而不一定需要全部使用Vue来开发整个 项目;
# Vue3.0 变化
1. 源码通过monorepo的形式来管理源代码:
- Mono:单个
pRepo:repository仓库
p主要是将许多项目的代码存储在同一个repository中;
- 这样做的目的是多个包本身相互独立，可以有自己的功能逻辑、单元测试等，同时又在同一个仓库下方便管理; p 而且模块划分的更加清晰，可维护性、可扩展性更强;
2. 源码使用TypeScript来进行重写
3. 使用Proxy进行数据劫持
- Vue2是使用Object.defineProperty来劫持数据的getter和setter方法的; 这种方式一致存在一个缺陷就是当给对象添加或者删除属性时，是无法劫持和监听的;
4. 由Options API 到 Composition API
5. Hooks函数增加代码的复用性

# 什么是CDN呢?(Content Delivery Network或Content Distribution Network)
- 它是指通过 相互连接的网络系统，利用最靠近每个用户的服务器;
- 更快、更可靠地将音乐、图片、视频、应用程序及其他文件发送给用户; -  来提供高性能、可扩展性及低成本的网络内容传递给用户;
### 常用的CDN服务器可以大致分为两种:
- 自己的CDN服务器:需要购买自己的CDN服务器，目前阿里、
腾讯、亚马逊、Google等都可以购买CDN服务器;
- 开源的CDN服务器:国际上使用比较多的是unpkg、 JSDelivr、cdnjs;
# 声明式和命令式
命令式编程关注的是 “how to do”，声明式编程关注的是 “what to do”，由框架(机器)完成 “how”的过程;

# methods方法绑定this
https://mp.weixin.qq.com/s/hYm0JgBI25grNG_2sCRlTA

# Vue内容回顾

## 一. 模板语法

### 1.1. 事件绑定 v-on用法

#### 1.1.1. v-on各种写法

* v-on:click="counter++"
* v-on:click
* @click
* 别的事件
* v-on="{click: xxxx}"

* 修饰符stop

```html 
    <div id="app">
      <!-- 1.基本写法 -->
      <div class="box" v-on:click="divClick">box--</div>
      <!-- 2.语法糖 -->
      <div class="box" @click="divClick">box--2</div>
      <!-- 3.绑定方法的位置,也可以写表达式 -->
      <h2>{{counter}}</h2>
      <button @click="increment">+1</button>
      <!-- 不推荐 -->
      <button @click="counter--">-1</button>
      <!-- 4.绑定其他方法 -->
      <div class="box" @mousemove="divMouseMove"></div>
      <!-- 5.绑定多个事件 -->
      <div class="box" @click="divClick" @mousemove="divMouseMove"></div>
      <!-- 不推荐 -->
      <div class="box" v-on="{ click:divClick,mousemove:divMouseMove}">11</div>
      <div class="box" @="{ click:divClick,mousemove:divMouseMove}">22</div>
    </div>
```



#### 1.1.2. 各种参数方式

* 默认传递 event

  ```
  1.如果该方法不需要额外参数，那么方法后的()可以不添加
  2.如果方法本身中有一个参数，那么会默认将原生事件event参数传递进去
  ```

  

* 自定义参数:
  
  * name, age, $event
  * 如果需要同时传入某个参数，同时需要event时，可以通过$event传入事件

```html
     <!-- 1.默认传递event对象 -->
      <button @click="btnClick">按钮1</button>
      <!-- 2.只传递自己的参数 -->
      <button @click="btnClick2('hello',1111)">按钮2</button>
      <!-- data里的变量 -->
      <button @click="btnClick3(info,name)">按钮2</button>
      <!-- 3.传递自己的参数和event对象 -->
      <!-- 在模板中想要明确的获取event对象: $event -->
      <button @click="btnClick4('哈哈哈哈',$event)">按钮3</button>
```



#### 1.1.3. 修饰符stop

* .stop - 调用 event.stopPropagation()  阻止冒泡
* .prevent - 调用 event.preventDefault()  阻止默认事件发生 ,比如a的href



### 1.2. 条件渲染

#### 1.2.1. v-if/else/else-if

* v-if="条件"
  * 当条件为false时，其判断的内容完全不会被渲染或者会被销毁掉； 
  * 当条件为true时，才会真正**渲染**条件块中的内容



#### 1.2.2. template元素

* template元素可以当做不可见的包裹元素，并且在v-if上使用，但是最终template不会被渲染出来
  * 可以在v-if和v-for上使用





#### 1.2.3. v-show

* if用法区别:
  * v-show不能和template结合
  * v-show不可以和v-else一起使用

* if的本质区别:
  * v-if为false元素会销毁/不存在
  * v-show为false元素的display none
* 选择:
  * 切换非常频繁使用v-show
  * 不频繁 v-if



## 二. 列表渲染

### 1.1. v-for的基本使用

* item in 数组
* (item, index) in 数组
* (item, index) of 数组

注意

* 注意上面的顺序：数组元素项item是在前面的，索引项index是在后面的

### 1.2. v-for其他的类型

* 对象
  * 一个参数： "value in object";
  * 二个参数： "(value, key) in object";
  * 三个参数： "(value, key, index) in object";
* 可迭代对象(字符串)
* 数字  
  * item in 10

```html 
<!-- 1.遍历数组 -->
      <ul>
        <li v-for="item in movies">{{item}}</li>
      </ul>
      <!-- 2.遍历对象 -->
      <ul>
        <li v-for="(value,key,index) in info">{{value}}--{{key}}--{{index}}</li>
      </ul>
      <!-- 3.遍历字符串,可迭代对象 -->
      <ul>
        <li v-for="item in message">{{item}}</li>
      </ul>
      <!-- 4.遍历数字 -->
      <ul>
        <li v-for="item in 100">{{item}}</li>
      </ul>
```



### 1.3. v-for绑定key属性

#### 1.3.1. VNode/虚拟DOM

* VNode

  ```
  1.VNode的全称是Virtual Node，也就是虚拟节点
  2.VNode的本质是一个JavaScript的对象
  3.template元素 ->解析成 VNode--->转换为真实DOM元素
  ```

* 虚拟DOM

  * template元素--->一个个VNode虚拟节点--->VNode Tree -->虚拟DOM--->真实DOM

  * 作用

    * 方便进行diff算法

    * 方便进行跨平台

      

* ```
  * template元素 -> VNode
  * 虚拟DOM作用之一:
    * 跨平台
  ```

  

#### 1.3.2. key的作用

* 有key的操作:
  * 根据key找到之前的VNode进行复用;
  * 没有VNode可以复用, 再创建新的VNode
* 没有key的操作:
  * diff算法, 后续VNode复用性就不强



#### 1.3.3. key绑定id

```html
      <ul>
        <!-- 注意;key 要求唯一,一般是id -->
        <li v-for="item in letters" :key="item">{{item}}</li>
      </ul>
```



## 三. Options API

### 3.1. 计算属性 computed

#### 3.1.1. 复杂数据的处理方式

* mustache插值语法自己写逻辑
* methods完成逻辑

```
思路一的实现：插值语法
缺点一：模板中存在大量的复杂逻辑，不便于维护（模板中表达式的初衷是用于简单的计算）；
缺点二：当有多次一样的逻辑时，存在重复的代码；
缺点三：多次使用的时候，很多运算也需要多次执行，没有缓存
```

```
思路二的实现：method实现
缺点一：我们事实上先显示的是一个结果，但是都变成了一种方法的调用；
缺点二：多次使用方法的时候，没有缓存，也需要多次计算
```



#### 3.1.2. 计算属性用法

* 计算属性
  * 可以通过this访问数据
  * 对于任何包含响应式数据的赋值逻辑,你应该使用计算属性
  * 计算属性默认对应的是一个函数

* 计算属性的用法

```js
       // 计算属性
        computed: {
          // 语法糖 --计算属性默认对应的是一个函数
          fullName() {
            return this.firstName + " " + this.lastName;
          },
          result() {
            return this.score > 60 ? "及格" : "不及格";
          },
          reverseMes() {
            return this.message.split(" ").reverse().join(" ");
          },
        },
```



#### 3.1.3. computed和methods区别

* computed底层会缓存, 性能更高
* 和method的区别
  * computed底层会缓存, 性能更高
  * 计算属性会基于它们的依赖关系进行缓存;
  * 在数据不发生变化时，计算属性是不需要重新计算的
  * 但是如果依赖的数据发生变化，在使用时，计算属性依然会重新进行计算
# Vue Cli





#### 3.1.4. computed的完整写法

* 计算属性在大多数情况下，只需要一个**getter**方法****即可，所以我们会将计算属性直接写成一个函数

* set  设置
* get   获取

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <!-- 1.拼接名字 -->
      <h2>{{fullName}}</h2>
      <button @click="editFullName">修改</button>
    </div>

    <script src="../lib/vue.js"></script>
    <script>
      // 1.创建app
      const app = Vue.createApp({
        // data: option api
        data() {
          return {
            firstName: "Maria",
            lastName: "Sklodowska-Curie",
          };
        },
        //methods: option api
        methods: {
          editFullName() {
            // 计算属性修改
            this.fullName = "li minghao";
          },
        },
        // 计算属性
        computed: {
          // 语法糖 --计算属性默认对应的是一个函数
          fullName() {
            return this.firstName + " " + this.lastName;
          },
          fullName: {
            get() {
              return this.firstName + " " + this.lastName;
            },
            set(newVal) {
              // 拆分
              const names = newVal.split(" ");
              this.firstName = names[0];
              this.lastName = names[1];
            },
          },
        },
      });

      // 2.挂载app
      app.mount("#app");
    </script>
  </body>
</html>

```



### 3.2. 侦听器 watch

#### 3.2.1. 基本侦听watch

* 侦听器: 在代码逻辑中监听某个数据的变化 

* 侦听器默认有两个参数:newValue,oldValue

  ```js 
  watch: {
            // 1,监听message
            // 默认有两个参数:newValue,oldValue
            message(newValue, oldValue) {
              console.log("watch message ,messag发生改变");
              console.log("newValue--", newValue);
              console.log("oldValue---", oldValue);
            },
   }
  ```

  

* 如果是对象类型, 那么拿到的是代理对象

  * Proxy对象转成原始对象
    * 方式一:   { ...newValue }
    * 方式二: Vue.toRaw(newValue)

  ```js 
  watch:{
           // 2.监听info
            info(newValue, oldValue) {
              // 2.如果是对象类型, 那么拿到的是代理对象
              console.log("info--newValue", newValue);
              console.log("info--oldValue", oldValue);
              //3.获取原始对象
              // 方式一:因为代理对象可迭代
              console.log({ ...newValue });
              console.log(Vue.toRaw(newValue));
            },
  }
  ```

  



#### 3.2.2. 侦听的选项

* deep    **深度监听**

  ```
  1.因为默认情况下，watch只是在侦听info的引用变化，对于内部属性的变化是不会做出响应的
  所以可以使用一个选项deep进行更深层的侦听(当info.name发生改变,也是可以监听到)
  2.watch里面侦听的属性对应的也可以是一个Object
  ```

  

* immediate    **希望一开始的就会立即执行一次**

  ```
  这个时候无论后面数据是否有变化，侦听的函数都会有限执行一次
  ```

  ```js 
  watch: {
          // 默认watch监听不会进行深度监听
          // info(newValue, oldValue) {
          //   console.log("侦听到info改变:", newValue, oldValue)
          // }
  
          // 进行深度监听
          info: {
            handler(newValue, oldValue) {
              console.log("侦听到info改变:", newValue, oldValue)
              console.log(newValue === oldValue)
            },
            // 监听器选项:
            // info进行深度监听
            deep: true,
            // 第一次渲染直接执行一次监听器
            immediate: true
          },
          "info.name": function(newValue, oldValue) {
            console.log("name发生改变:", newValue, oldValue)
          }
        }
  ```

  



#### 3.2.3. 其他的写法

* "info.name"
* 别的写法
* created -> this.$watch()

```
created 生命周期回调函数: 当前的组件被创建时自动执行
一般在该函数中, 会进行网络请求
```



```html 
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>

  <div id="app">
    <h2>{{message}}</h2>
    <button @click="changeMessage">修改message</button>
  </div>
  
  <script src="../lib/vue.js"></script>
  <script>
    // 1.创建app
    const app = Vue.createApp({
      // data: option api
      data() {
        return {
          message: "Hello Vue"
        }
      },
      methods: {
        changeMessage() {
          this.message = "你好啊, 李银河!"
        }
      },
      // 生命周期回调函数: 当前的组件被创建时自动执行
      // 一般在该函数中, 会进行网络请求
      created() {
        // ajax/fetch/axios
        console.log("created")

        this.$watch("message", (newValue, oldValue) => {
          console.log("message数据变化:", newValue, oldValue)
        }, { deep: true })
      }
    })

    // 2.挂载app
    app.mount("#app")
  </script>
</body>
</html>
```





















