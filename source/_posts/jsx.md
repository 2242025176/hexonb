---
    title: jsx语法
    date: 2021-07-08
    categories: react #分类
    tags: jsx  #标签
---

# **1.jsx的基本使用**

## **1.1 createElement() 的问题：**（react不用jsx渲染的渲染方法）

> 繁琐不简洁
>
> 不直观，一眼看不出 渲染的 元素到底是什么结构
<!-- more --> 
```jsx
 const title = React.createElement(
        'h1',
        {title:'我是h1',id:'h1'},
        'hello,react',
        React.createElement(
            'span',
            null,
            '我是span'
        )
    )
//渲染
ReactDOM.render(title,document.getElementById('root'))
```

## **jsx的实现：**

```jsx
<h1>
    hello,react
    <span>我是span<span>
</h1>
```

## **1.2 jsx 简介：**

**jsx** 是 javascript XML的简写，表示在javascript 代码中写 XML（html）格式的代码。

在普通html 或其他 项目 是不能 使用jsx的

## **1.3 使用步骤：**

1.使用jsx语法创建 react 元素

```jsx
const title = <h1>hello</h1>
```

2.渲染到页面还是 使用 ReactDOM.render() 方法

```jsx
ReactDOM.render(title,document.getElementById('root'))
```

## **1.4 注意点：**

> 1.ract 元素的属性名使用驼峰命名法；
>
> 2.特殊属性名： class -> className  for -> htmlFor    tabindex -> tabIndex
>
> 3.推荐`小括号`包裹 jsx （），避免js中的自动插入分号的陷阱。

```jsx
const title = (
    <h1 className='title'> // 如果写 class 会报错 
        hello jsx
        <span/>
    </h1>
)
```

## **2. 在jsx 中使用javascript 表达式**

**嵌入js 表达式**

> 1.数据存储在 js 中
>
> 2.语法：{ js表达式 }
>
> 3.{} 中是不能使用 for || if 这样的语句的

```jsx
const name = '哈哈哈' //表达。
//jsx 创建元素：
const title = (
    <h1 className='title'>
        hello jsx {name}
    </h1>
)
```

**函数调用表达式：**

```jsx
// 函数调用表达式
const sayhi = () => 'hello'
//jsx 创建元素：
const title = (
    <h1 className='title'>
        {sayhi()} // hello
    </h1>
)
```

**还有一些基本的 运算：**

```jsx
//jsx 创建元素：
const title = (
    <h1 className='title'>
        {1 + 7}   // 8
        {3 > 8 ? "大于" : '小于等于'} // 小于等于
    </h1>
)
```

**jsx 自身也是 js 表达式：**

```jsx
const av = (<div>我是div</div>)
//jsx 创建元素：
const title = (
    <h1 className='title'>
        {av}  //这里就会把 div 渲染出来。
    </h1>
)
```

## **3.jsx 条件渲染**

1.判断 加载状态 

```jsx
const isloding = false
const longding = () => {
    if(isloding){   
        return <div>加载中。。。</div>
    }
    return (<div>加载完成</div>)
}

//jsx 创建元素：
const title = (
    <h1 className='title'>
       {longding()}  // 因为状态是false 返回的<div>加载完成</div>
    </h1>
)
```

2.使用 三目运算 实现：以上效果 

```jsx
const isloding = true // 全局状态 
const longding = () => {
  return isloding ? (<div>加载中。。。</div>) : (<div>加载完成</div>)
}
//jsx 创建元素：
const title = (
    <h1 className='title'>
       {longding()}  // 因为状态是true 返回的<div>加载中。。。</div>
    </h1>
)
```

3.使用&& 运算符：

> && 状态为 true ， 才会执行  为 false 就会中断 执行

```jsx
const isloding = true
const longding = () => {
  return isloding && (<div>加载中。。。</div>) 
}
const title = (
    <h1 className='title'>
       {longding()}  // 因为状态是true 返回的<div>加载中。。。</div>
    </h1>
)
```

## **4.列表渲染：**

如果要渲染 数组 对象形式的列表数据，可以使用数组 `map()` 方法。

注意： 渲染列表 要添加 `key` 属性，和vue 一样 key 要保证是唯一值。

案例：

```jsx
const list = [
    {id:1,name:'吴海东1'},
    {id:2,name:'吴海东2'},
    {id:3,name:'吴海东3'}
]
//jsx 创建元素：
const title = (
    <h1 className='title'>
       {list.map(item => <li key={item.id}>{item.name}</li>)}
    </h1>
)
```

## **5.jsx 样式处理：**

1.行内样式 -- style 

```jsx
const title = (
    <h1 style={{color:"red",background:'#000'}}>
       jsx 的样式处理
    </h1>
)
```

2.类名 ---  className方法：

创建index.css:

```css
.title{
    text-align: center;
}
```

引入：

```jsx
// 引入 css
import './css/index.css'

//jsx 创建元素：
const title = (
    <h1 className='title'>
       jsx 的样式处理
    </h1>
)
```

