---
    title: vue-router-路由
    date: 2021-07-3
    categories: vue #分类
    tags: vue  #标签
---


#  vue路由：

当前vue-cli的版本是 4.5.9 版本；

在生成项目的时候 可以自行选择需要自动配置路由还是 自己手动配置；当然 直接让他配置;

#### 注：component: () => import('组件路径')  这一步是vue路由的懒加载   不用在文件import导入在配置 这一行代码一步到位

当前版本的路由 找到 根目录下的 router /index.js

```js
const routes = [
  {
    path: '/', 
    name: 'Home',
    component: () => import(/* webpackChunkName: "about" */ '../views/Home.vue')
  },
  {
    path: '/about',
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]
```

配置好后在 app.vue 里：使用

```html
 <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>

<!-- 路由匹配到的组件将显示在这里 -->
  <router-view></router-view> <!-- 简单来讲就是在这里展示页面 就像tab切换一样-->
```

## 6.1 嵌套路由：

#### 通过配置children方法可实现多层子路由的嵌套

router /index.js：↓

```js
const routes = [
  {
    path: '/',
    name: 'Home',
    // component: Home
    component: () => import(/* webpackChunkName: "about" */ '../views/Home.vue')
  },
  {
    path: '/about',
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue'),
    children:[  //在about下嵌套两个子页面
      {
        path:'log',
        name:'Log',
        component: () => import(/* webpackChunkName: "about" */ '../views/log/log.vue'),
      },
      {
        path:'logs',
        name:'Logs',
        component: () => import(/* webpackChunkName: "about" */ '../views/log/logs.vue'),
      }
    ],
  }
]
```

About.vue : ↓

```html
<router-link :to="{name: 'Log'}" tag="li" >我的收藏1</router-link> 
<!-- 可以根据路径 也可以根据name   这个就是 官网的命名路由-->
<router-link :to="{name: 'Logs'}" tag="li" >我的收藏2</router-link>
<!-- 路由匹配到的组件将显示在这里 -->
<router-view></router-view>
```

## 6.2 编程式路由：参考：https://blog.csdn.net/crazywoniu/article/details/80942642

| 声明式：↓                 | 编程式：↓          |
| ------------------------- | ------------------ |
|                           |                    |
| `<router-link :to="...">` | `router.push(...)` |

### 第一种传参方式：

      某个vue组件：

```js
this.$router.push({name: 'Home', params: { userId: '路由传参 登录页面的参数' }});
```

Home.vue：

		接收：

```html
<div>{{this.$route.params.userId}}</div>
```



## 6.3 路由命名视图：

## 参考：https://blog.csdn.net/weixin_31765427/article/details/77882703



router/index.js:

```js
import Vue from 'vue'
import Router from 'vue-router'
import Goodlists from '@/Goodlists/goods'
import Title from '@/Goodlists/title'
import Img from '@/Goodlists/img'
Vue.use(Router)
export default new Router({
  routes: [
    {
      path: '/goods',
      name: 'Goodlists',
      components:{
        default:Goodlists, //默认展示的页面
        title:Title, 
        image:Img,
      } 
     } 
  ]
})
```

app.vue: 

```html
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>   <!-- 默认展示的页面 -->
    <router-view name="title" class="left"></router-view> <!-- 根据配置的命名渲染组件-->
    <router-view name="image" class="right"></router-view><!-- 根据配置的命名渲染组件 -->
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>
```

效果图：

![这里写图片描述](https://img-blog.csdn.net/20170907155353635?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzMxNzY1NDI3/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 6.4 路由组件传参：

分为：布尔模式 、对象模式、函数模式。

## 6.5 过渡动效：

所以我们可以用 `<transition>` 组件给它添加一些过渡效果：

可参考本页面第三章下的第一条

## 6.6 路由懒加载：

刚开始已经提到了  这里还是说一下：

非懒加载：你得一个一个组件往里面导入：

![img](https://img-blog.csdnimg.cn/20190306112009295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3htMTAzNzc4Mjg0Mw==,size_16,color_FFFFFF,t_70)

懒加载：不需要 impore 一个一个导入了直接：当前vue-cli的版本是 4.5.9 版本

![img](https://img-blog.csdnimg.cn/20190306112040195.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3htMTAzNzc4Mjg0Mw==,size_16,color_FFFFFF,t_70)

## 6.7 路由导航守卫：

#### 6.7.1 全局前置守卫   router.beforeEach（）

```
beforeEnter(to,from,next)
// to  要进入的目标，路由对象
// from 当前导航正要离开的路由
// next 初步认为是展示页面；（是否显示跳转页面）
```

参考：https://blog.csdn.net/heshuaicsdn/article/details/88020796

router.beforeEach（）一般用来做一些进入页面的限制。比如没有登录，就不能进入某些页面，只有登录了之后才有权限查看某些页面。。。说白了就是路由拦截。

## 第一步 规定进入路由需不需要权限:

@/router/index.js

```js
 
{
    path: '/',
    name: 'Home',
    components:{  
      default:Home,
      log:Log
    } ,
    meta : {                      //加一个自定义obj
      requireAuth:true      //这个参数 true 代表需要登录才能进入home
   	}
},
```



## 第二步 使用vuex整一个userId:

stire/index.js

```js
export default new Vuex.Store({  //定义vuex存储
  state: { //放置所有的状态    //Getter 接受 state 作为其第一个参数：
    userId : '0'
  },
// 状态三 同步提交 更改 state 状态
  mutations: {
    logo(state,step){
      state.userId = step
    }
  },
  //状态4  异步更改  state 状态  Action 提交的是 mutation，而不是直接变更状态
  actions: {
    logo(context,stop){
      context.commit('logo',stop)
    }
  }
}
)
```

## 第三步 使用router.beforeEach()

min.js

```js
router.beforeEach((to,from,next)=>{
	if(to.meta.requireAuth){
        console.log(store.state.userId) //当点击登录router跳转的时候 这步就会执行 看状态是不是1
		if(store.state.userId == 1){ 
			next()
		}else{
			next({path:'/longes'})
		}
	}else{
		next()
	}
})
```

## 第四步: 在longes 组件登录 因为当前状态是0 所以进不去home页面（）：

longes组件：

```html
<template>
  <div>
      登录界面-您当前还没有登录
      <button @click="logos">登录</button>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
data(){
    return{}
},
methods:{
    ...mapActions(['logo']),
    logos(){
        this.logo(1) //给Action 传参 进行state下的userId进行更改
        this.$router.push({path:'/'}) 
    }
}
}
</script>
```



#### 6.7.2 路由独享守卫

你可以在路由配置上直接定义 `beforeEnter` 守卫：

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

这些守卫与全局前置守卫的方法参数是一样的。

#### 6.7.3 组件内守卫（指在vue组件内的守卫）

参考博客：https://www.cnblogs.com/qdwds/p/11516247.html

最后，你可以在路由组件内直接定义以下路由导航守卫：

- `beforeRouteEnter`
- `beforeRouteUpdate` (2.2 新增)
- `beforeRouteLeave`

about.vue :

```js
<script>
export default {
  name: 'about',
  data(){
    return{
      num:10
    }
  },
  	    beforeRouteEnter:(to,from,next)=>{ //进入这个组件时触发
            next(vm=>{
                alert(vm.num)//  通过 `vm` 访问组件实例
            })
        },
        beforeRouteUpdate (to, from, next) { //触发条件 路由更新的时候 会触发 (指在本页面跳转)
              this.name = to.path
              next()
		},
        beforeRouteLeave (to, from, next) {//离开这个组件时触发
            if(confirm('确定离开吗？') === true){
                next()
            }else{
                next('aa')
            }
        }
}
</script>
```