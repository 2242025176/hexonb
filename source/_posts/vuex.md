---
    title: vuex-状态管理
    date: 2021-07-3
    categories: vue #分类
    tags: vue  #标签
---

# Vuex 

# 1.state

- #### 	state是提供唯一的公共数据源；（简单来说 所有组件都可以拿 state 定义的 对象 里的参数：）

### 1.2 访问state 对象参数的第一种方法：

```js
this.$store.state.你定义的全局name
```

### 1.3 访问state 对象参数的第二种方法：

```js
#绑定
<div>{{count}}</div> 
#导入
import { mapState } from 'vuex' 
#访问
computed:{
        ...mapState(['count']) 
}
```

​	通过导入 `mapstate` 函数，将当前组件需要的全局数据，映射为当前组件的 `computed `计算属性

# 2. Mutation

- ### 更改 Vuex 的 store 中的状态、的`唯一方法`是提交 mutation。

- 注：不要在 mutations  里执行异步操作；

  ​		简单理解异步操作 ：异步api 往往 都会有回调函数 

#### 2.1 更改store 中的状态   （定义 mutations 里的 更改方法（add）） ：

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    add(state) {    
      // 变更状态
      state.count++  #当然也可以=赋值更改状态
    }
  }
})
```

#### 		在组件中触发 mutations 里定义的add方法 ，`第一种`方法：commit 唤醒	（让count++）

```js
 methods:{
        btn(){
            this.$store.commit('add');
        }
    }
```



#### 2.2  在触发 mutations  时传递参数：

- ### 		你可以向 `store.commit`  传入 `额外的参数` 用官方的话说叫	提交载荷（Payload）

####        事件触发 mutations 里定义的addN  并 携带 参数

```js
 methods:{
        btn2(){
            this.$store.commit('addN',5); #额外参数是指这个5 ，当然你可以传其他参数绑定到state参数上
        }
    }
```

```js

const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    addN(state,step) {# state就是全局状态  step 接收到的参数
      // 变更状态
      state.count += step  #当每次触发的时候 都 +5 ,可以根据需求传递 绑定
    }
  }
})
```

#### 在组件中触发 mutations 里定义的方法的`第二种`方法：	（让count更改）

- #### 在组件中引用

```js
import { mapMutations } from 'vuex'
```

- #### 使用 `mapMutations` 辅助函数将组件中的 methods (方法)映射为 `store.commit` 调用

```js
 methods:{
         ...mapMutations(['add','addN']),
        etn1(){ #按钮点击事件 触发 add() && addN() 都是mutations 里定义的方法
           this.add()
           this.addN(5)//当然也是可以传参的
        },
    },
```

# 3. Action

Action 类似于 mutation，不同在于：

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。mutation不支持执行异步操作。

## 3.1使用actions 更改 state 里的状态；



```js
 mutations: {
    add (state) {
      //state 的打印结果 是 上面 state 对象 
      state.count++
    }
 }

actions: {
    add(context) {
      //在actions 不能直接更改 状态
      //必须通过 context.commit() 触发某个  mutations 才行
      setTimeout(()=>{
        context.commit('add') # 这里的 commit 触发 mutations 里的 add
      },1000)
    }
  }
```



```js
	btn3(){
            //dispatch 专门用来触发 actions
            this.$store.dispatch('add');	#这里的 dispatch 触发 actions 里的 add
        }
```

## 3.2 触发 actions 的时候 携带参数 第一种方法；

```js
mutations: {
    addN(state,step){
      state.count += step
    },
 }  
actions: {
    addN (context,stop) { # stop 就是 触发传 过来的参数
      setTimeout(()=>{
        context.commit('addN',stop)# 这里的 commit 触发 mutations 里的 addN 并传参
      },1000)
    }
  }
```

```js
btn4(){
            //dispatch 专门用来触发 actions
            this.$store.dispatch('addN',5);	#这里的 dispatch 触发 actions 里的 addN
        }
```

## 3.3 触发 actions 的时候 携带参数 第二种方法；

```js
 mutations: {
    subN(state,step){
      state.count -=step
    }
  },
 
 actions: {
   subN(context,stop){
        setImmediate(()=>{
          context.commit('subN',stop)
        },1000)
  	}
  }
```

​	在页面中引用：

```js
import {mapActions} from 'vuex'
```

​	调用：

```js
 methods:{
         ...mapActions(['subN']),
         etn4(){
           this.subN(5)
        },
    },
```

# 4. Getter:

- Getter 用于对state 中的数据进行加工返回新的数据；
- 类似于 vue 计算属性。

```js
getters: {  // getters  vuex的计算属性
        shhow(state){
          return '当前最新的数量'+state.count
        }
  },
  

```

调用getters>shhow   第一种方法

```js
  this.$store.getters.shhow
  #在html中可直接：
  <div>{{$store.getters.shhow}}</div>
```

调用getters>shhow   第二种方法

导入：

```js
import {mapGetters} from 'vuex'
```

在计算属性中：

```js
computed:{
        ...mapGetters(['shhow'])
    }

在html中 直接引用 
<div>{{shhow}}</div>
```

# 5.Module 

当应用变得非常复杂时，store 对象就有可能变得相当臃肿。

为了解决以上问题，Vuex 允许我们将 store 分割成**模块（module）**。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：官方示例

```js
const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```