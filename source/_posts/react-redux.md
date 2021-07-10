---
    title: react-redux
    date: 2021-07-07
    categories: react #分类
    tags: redux  #标签
---

# React-redux



> react-redux 是 redux 官方出的配合 react 绑定的库

> react-redux 可以 让开发者 很容易从 redux store 中读取数据，并向store中分发 actions 以此来更新数据
<!-- more --> 
# 安装 React Redux

Redux 默认并不包含 [React 绑定库](https://github.com/reactjs/react-redux)，需要单独安装。

```Bash
npm install --save react-redux
```

# 核心的两个方法

# 1.Provider：

`provider`包裹在根组件外层，使所有的子组件都可以拿到`state`。

# 2. connect:

如果我们要接收 provider 中的 store ，就需要我们把组件通过 connect 加强。

#### connect 的第一个参数是 `mapStateToProps`

这个函数允许我们将 store 中的数据作为 props 绑定到组件上

**connect 的第二个参数是 ****`mapDispatchToProps`**

由于更改数据必须要触发`action`, 因此在这里的主要功能是将 `action` 作为`props` 绑定到 组件上

# 实践加减案例

### 1. 构建 reducer /index.js

```JavaScript
/*
    这个文件是 创建 reducer 函数的，专门用来处理 发送过来的 action
*/ 

const initState = { //默认状态
    value: 0 
}
// 第一个参数是 state ，第二个参数 是 action （action是返回过来的参数状态）
const reducer = (state = initState,action) => {
    //判断
    switch (action.type) {
        case 'add_action':
            return {
                value:state.value + 1
            }
        default:
            return state;
    }
}
module.exports = {
    reducer
}
```

### 2. 构建 store

在我看来 store 就是输出 状态 的一个环节

```JavaScript
import {createStore} from 'redux'

// 导入我们自己创建好的 reducer
import {reducer} from '../reducer'

// 利用createStore来构建 store
const store =  createStore(reducer)

export default store;
```

### 3.构建pages文件夹并在在pages下构建 home（按钮）组件 和 link （显示 +1 状态）组件

home：组件 主要是发送状态

```JavaScript
import React from 'react';

// 导入 connect 

import {connect} from 'react-redux'
class Index1 extends React.Component{
    constructor(props){
        super(props);
        this.state = {

        }
    }
    home = () =>{
        // console.log('拿到定义的 sendAction 方法',this.props);
        // 发送 action 
        this.props.sendAction()
    }
    render(){
        return(
            <div>
                <button onClick={this.home}>按钮+</button>
            </div>
        )
    }
}
//这个函数要有一个返回值，返回值是一个对象（要发送的 action）
const mapDispatchToProps = (dispath) =>{
    return{
        sendAction:() =>{
            //利用dispath 发送一个action   (更新状态的方法)
            // 传递action 对象 我们要定义一个 type属性
            dispath({
                type:'add_action'
            })
        }
    }
}
// home  是发送方所以使用mapDispatchToProps方法 
// connect(接收的函数,要发送的action的函数)(放入要加强的组件)
export default connect(null,mapDispatchToProps)(Index1)
```

link 组件： 主要是展示 接收 修改后的状态

```JavaScript
import React from 'react';
// 导入 connect
import {connect} from 'react-redux'

class Index2 extends React.Component{
    render(){
        return(
            <div>{this.props.value}</div>
        )
    }
}
//接收两个参数
const mapStateToProps = (state) =>{
    // console.log("link",state);
    return state;
}
// link 属于接收 所以使用第一种方法：mapStateToProps 
// connect(接收的函数,要发送的action的函数)(放入要加强的组件)
export default connect(mapStateToProps)(Index2)
```

### 4.在app.js 中展示：

Provider 包裹整个组件 ，使得所有组件都可以拿到 ，redux 共享的状态

```JavaScript
import React from 'react';
import Index1 from './pages/home/index'// 按钮
import Index2 from './pages/link/index'// 状态
import store from './store' //返回 处理 后的 数据
//导入 provider 组件，利用这个组件包裹我们的结构，从而能够达到统一 维护stroe 的效果
import {Provider} from 'react-redux'
function App() {
  return (
    <Provider store={store}>
      <div className="App">
        <Index1></Index1>
        <Index2></Index2>
      </div>
    </Provider>
  );
}

export default App;
```