---
    title: vue常用
    date: 2021-07-3
    categories: vue #分类
    tags: vue  #标签
---


# vue常用命令



## 1.生命周期：



```javascript
**beforeCreate**: function (){},   //在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

  **created**: function (){},   //在实例创建完成后被立即调用。

  **beforeMount**: function (){},   //在挂载开始之前被调用：相关的 render 函数首次被调用。

  **mounted**: function (){},   //el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。

  **beforeUpdate**: function (){},    //数据更新时调用，发生在虚拟 DOM 打补丁之前。

  **updated**: function (){},      //由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

  **beforeDestroy**: function (){},    //实例销毁之前调用。在这一步，实例仍然完全可用。

  **destroyed**: function (){} //Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。},

============================================================================================

activated:function(){} //被 keep-alive 缓存的组件激活时调用。

deactivated:function(){} //被 keep-alive 缓存的组件停用时调用。

Vue.config.errorHandler = function (err, vm, info) {
  #处理错误信息, 进行错误上报
  #err错误对象
  #vm Vue实例
  #`info` 是 Vue 特定的错误信息，比如错误所在的生命周期钩子
  #只在 2.2.0 + 可用
}
当捕获一个来自子孙组件的错误时被调用。
# 此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。
此钩子可以返回 false 以阻止该错误继续向上传播。

```

# 2.常用的vue方法：

#### 2.1 v-if && v-show (可控制元素的显示||隐藏)

```vue


<div v-if='datares'>块元素</div> //这里就会根据 true || false 来显示或隐藏 当然也可以进行条件的判断

<div v-else >显示</div> //else 当if条件不成立 在执行这一步 ，如还有判断条件 v-else-if 可以继续加条件

<div v-show='datares'>块元素</div> //v-show 也是同理 区别在于 v-show是用css样式控制显示隐藏 if是销毁、创建

data(){
	return{
		datares:true
	}
}
```

### 2.2  v-text ：

```html
<span v-text="msg"></span>
    //和下面的一样 v-text && {{}} 绑定效果是一样的 
 <span>{{msg}}</span>
```

#### 2.3 v-html （解析html结构的参数）

```vue
<div v-html="html"></div>

data(){
    return{
      html:`
        <div>
          <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
          </ul>
        </div>
     `
    }
  }
```

#### 2.4 v-for （循环渲染）&& ：key（基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。）

```vue
<div v-for="(item,index) in listObj" :key="item.id">{{item.name}}</div>

data(){
    return{
     listObj:[
        {id:1, name:'zs1'},
        {id:2, name:'zs2'},
        {id:3, name:'zs3'},
        {id:4, name:'zs4'},
        {id:5, name:'zs5'},
        {id:6, name:'zs6'},
      ]
    }
  },
```

#### 2.5  v-on && v-bind （问答：两种绑定 有什么不同呢）

			v-on 指令用于绑定HTML事件 ：v-on:click 缩写为 @click

```vue
<!-- 完整语法 -->
<a v-on:click="doSomething">123</a>

<!-- 缩写 -->
<a @click="doSomething">123</a>
```

			v-bind指令用于设置HTML属性：v-bind:href 缩写为 :href

```vue
<!-- 完整语法 -->
<a v-bind:href="url">123</a>

<!-- 缩写 -->
<a :href="url">123</a>
```

#### 2.6 v-model （双向绑定）

	v-model 它能轻松实现表单输入和应用状态之间的双向绑定

```vue
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>

data: {
    message: 'Hello Vue!'
}
```

#### 2.7 新增 v-slot （插槽）参考：https://blog.csdn.net/liushijun_/article/details/92186739

### [scope 移除](https://cn.vuejs.org/v2/api/?#scope-移除)

### [slot 废弃](https://cn.vuejs.org/v2/api/?#slot-废弃)

### [slot-scope 废弃](https://cn.vuejs.org/v2/api/?#slot-scope-废弃)

```vue

//index.vue组件调用MyFooter.vue
<MyFooter v-red :age.sync="age">
  <template v-slot:footer>
  //这里v-slot：后边的值与组件内的slot的name属性对应，也就是插槽的名称。
      <div>list</div>
  </template>
</MyFooter>

//MyFooter.vue组件
<template>
    <div>
        {{age}}
        <div>
            <slot name='footer' />
            //这里name的值就是这个插槽的名称。
        </div>
    </div>
</template>
```

#### 2.8 v-pre （跳过元素编译）：

```vue
<span v-pre>{{msg}}</span>     即使data里面定义了msg这里仍然是显示的{{msg}}
```

#### 2.9 v-cloak （解决）：参考：https://www.jianshu.com/p/f56cde007210?utm_source=oschina-app

		当网络较慢，网页还在加载 Vue.js ，而导致 Vue 来不及渲染，这时页面就会显示出 Vue 源代码。我们可以使用 v-cloak 指令来解决这一问题。

#### 2.10 v-once （使用了v-once指令的p元素不会随之改变）

```vue
		<p v-once>{{msg}}</p>  //msg不会改变
		<p>{{msg}}</p>
		<input type="text" v-model = "msg" name="">
		-------------------------------------------------
		data : {
				msg : "hello"
			}
```

#### 2.11  ref方法：参考：https://www.jianshu.com/p/623c8b009a85

`ref`基本用法 获取页面`dom`

```vue
 <div ref="testDom">11111</div>
 ----------------------------------
 console.log(this.$refs.testDom)//打印结果：<div>11111</div>
```

获取的`dom`的方法还有 `$event`

`$event`是指当前触发的是什么事件（鼠标事件，键盘事件等）;

`$event.target`则指的是事件触发的目标，即哪一个元素触发了事件，这将直接获取该dom元素



#### 2.12  is 方法 && 内置组件 [component ](https://cn.vuejs.org/v2/api/#component)依赖于is，来决定哪个组件被渲染。

```vue
<p is='MyFooter'></p> //MyFooter是指导入的 子模块  从而用这个p 标签渲染出子模块的内容

```



# 3.内置组件：

#### 3.1.transition && transition-group：

#### 	官网提供经典案例：https://cn.vuejs.org/v2/guide/transitions.html

		Vue 提供了 `transition` 的封装组件，可以给任何元素和组件`添加进入/离开过渡`

使用条件：

- 条件渲染 (使用 `v-if`)
- 条件展示 (使用 `v-show`)



#### 3.2. keep-alive：

这篇文章比较易懂：https://www.jianshu.com/p/4b55d312d297

被包裹在keep-alive中的组件的状态将会被保留，例如我们将某个列表类组件内容滑动到第100条位置，那么我们在切换到一个组件后再次切换回到该组件，该组件的位置状态依旧会保持在第100条列表处：

```vue
<keep-alive>
    <loading></loading>
</keep-laive>
```



## 4.watch监听:

	监测 Vue 实例变化：回调函数得到的参数为新值和旧值；

例子：

html:

```html
<input type="text"  v-model="a" />
<input type="text"  v-model="b.c" />
```

js:

```js
data() {
    return {
      a: 1,
      b:{
      	c:2
      }
    };
  },
watch: {
    //普通监听：
    a(val, oldVal) {
      console.log("a:" + val, oldVal);
    },
     //深度监听，可监听到对象、数组的变化
    b: {
      handler(val, oldVal) {
        console.log("b.c: " + val.c, oldVal.c);
      },
      deep: true, //true 深度监听
    },
  },
```



## 5.computed 计算属性：

官方介绍：

	在模板中放入太多的逻辑会让模板过重且难以维护。例如：

```html
<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
```

	所以，对于任何复杂逻辑，你都应当使用**计算属性**。

计算属性使用例子：

html：

```html
<div id="example">
  <p>Original message: "{{ message }}"</p> //message 绑定的data 里面的数据
  <p>Computed reversed message: "{{ reversedMessage }}"</p> //直接绑定的计算属性的方法
</div>
```

js:

```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('') //计算完成后 返回给方法reversedMessage
    }
  }
})
```

结果：

- Original message: "Hello"
- Computed reversed message: "olleH"

## 5.vue 的子父传参：

### 	5.1：父向子传参：

**情况一：父组件给子组件传值方法，使用props **  参考：https://www.cnblogs.com/phermis/p/10710894.html

父组件：

```html
<template>
    <div class="sidebar_contianer">
        <sidebar-item :routerData="transmitData"></sidebar-item>
    </div>
</template>
<script>
import sidebarItem from './sidebarItem'
export default {
    data(){
        return{
            transmitData:{
                title:'首页',
                uuid:'123'
            }
        }
    },
    components:{
        sidebarItem //注册组件
    }
}
</script>
```

子组件：

```js
<script>
export default {
    name:'sidebarItem',
    props:{
        transmitData:{
            type:Object,
            default:null
        }
    }
}
</script>
```

## 5.2 子向父传参：

**情况二：子组件要给父组件传值方法，使用$emit **  触发父组件的方法从而 返回回调 

子组件：

```html
<template> 
    <div class="testCom">
        <input type="text" v-model="message" />
        <button @click="click">发送消息给父组件</button>
    </div>
</template>
<script>
export default {
    data() {
        return {
          message: '我是来自子组件的消息'
        }
    },
    methods: {
      click() {
            //1、childFn 组件方法名，父组件中用childFn方法接收子组件中的数据；2、message是传递给父组件的数据
            this.$emit('childFn', this.message);
        }
    }    
}
</script>
```

父组件：

```html
<template>
    <div>
      <child-com @childFn="parentFn"></child-com>
    </div>
</template>

<script>
export default {
    // ...
    data: {
        message: ''
    },
    methods: {
       parentFn(childData) {  //$emit  触发 方法parentFn 
        this.message = childData;
      }
    }
}
</script>
```



#### 