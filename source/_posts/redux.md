---
    title: redux
    date: 2021-07-07
    categories: react #分类
    tags: redux  #标签
---

## 1.redux 是什么？

>    简单明了的说明，就是`状态管理`。

注： react 和 redux 是没有关系的，redux 可以 在 javascript 、jquery 等等，语言或框架中使用

### **redux中文文档：**http://cn.redux.js.org/

### 使用场景：

- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
- 一个组件需要改变全局状态
- 一个组件需要改变另一个组件的状态

## 2.使用redux

1. 在本地项目安装：（命令）

```Bash
npm install --save redux
```

1. 核心模块

# 1.创建一个Action

- 在src 目录下 创建 `action/index.js` 文件

构建action 函数：（定义状态的 函数）

```JavaScript
/*
    action 的构建函数
*/ 

const sendAction  = () =>{
    return{
        type:"send_type",
        value:"我是一个action"
    }
}

module.exports = {
    sendAction
}
```

# 2.创建 Reducer

在src 目录下 创建 `reducer/index.js` 文件

这个文件是 创建 reducer 函数的，专门用来处理 发送过来的 action

```JavaScript
/*
    这个文件是 创建 reducer 函数的，专门用来处理 发送过来的 action
*/ 
const initState = {
    value:"没有action状态，就上这个默认值"
}
const reducer = (state = initState,action) => {
    switch (action.type) {
        case 'send_type':
            return Object.assign({},state,action)
        default:
            return state;
    }
}
module.exports = {
    reducer
}
```

### 为了好理解 这里 说一下 ES6 的`Object.assign()`方法:

`Object.assign()` 是 浅拷贝 类型的方法

下面案例 是 复制了一个对象 然后赋值给 copy

```JavaScript
// 案例一
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
// 案例二
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const copy = Object.assign({}, obj1,obj2);
console.log(copy); // { a: 1,b:2 }
```

# 3.创建Store

在src 目录下 创建 `store/index.js` 文件；

**Store** 就是把它们联系到一起的对象。Store 有以下职责：

- 维持应用的 state (状态)；
- 提供 [`getState()`](http://cn.redux.js.org/docs/api/Store.html#getState) 方法获取 state；
- 提供 [`dispatch(action)`](http://cn.redux.js.org/docs/api/Store.html#dispatch) 方法更新 state；
- 通过 [`subscribe(listener)`](http://cn.redux.js.org/docs/api/Store.html#subscribe) 注册监听器;
- 通过 [`subscribe(listener)`](http://cn.redux.js.org/docs/api/Store.html#subscribe) 返回的函数注销监听器。

Redux提出了(公用的)Store的概念来管理数据。

```JavaScript
import {createStore} from 'redux'

// 导入我们自己创建好的 reducer

import {reducer} from '../reducer'

// 构建 store
//createStore 的返回值就是我们构建好的 store 然后进行导出，
// 
const store =  createStore(reducer) 

export default store;
```

# 4.在某个组件输出状态：

也在src 下 创建 `pages/home/index.js`

```JavaScript
import React from 'react';
// 导入 store 输出状态
import store from '../../store'
// 导入 action 构建函数 （全局状态）
import {sendAction} from '../../action'

class Index extends React.Component{
    home = () =>{
        const action = sendAction();
        // console.log('点击 ');
        store.dispatch(action) // dispatch(action) 方法更新状态。（不更新的话 输出的是默认状态）
    }
    // 当组件一加载完成的时候 来监听
    componentDidMount(){
        store.subscribe(() =>{
            console.log("reducer 处理之后的值",store.getState()); // reducer 处理之后的值
            this.setState({}) // 更改状态 因为没有要更改的状态 所以传一个空对象 不加这个会出现视图容器不更新的问题
        })
    }
    render(){
        return(
            <div>
                <button onClick={this.home}>按钮-发送一个action</button>
                <div>{store.getState().value}</div>
            </div>
        )
    }
}

export default Index
```

> 这里 总的可以 理解 ：

1.Action 存储状态 、

1. Reducer 处理拿到的Action状态 、

3.Store 就可以将处理之后的 Action 状态输出到某个组件中