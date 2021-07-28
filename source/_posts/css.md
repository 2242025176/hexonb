---
    title: css常用
	top: 4
    date: 2021-06-27 #发布时间
    categories: css #分类
    tags: css  #标签
	
---

## 一、css的方法和选择器用法：

## 1.浮动：

> ###### 搭建普通的pc端网页用到的比较多，现在都是一套两端页面的这种`媒体查询`的模式，使用浮动的地方远远下降了许多

```css
float:right;/* left  right  none*/
```

清除浮动的方法：（不止以下两种方法）

> 1. 给父级加高
> 2. 父级使用overflow: hidden;属性

不清除浮动会造成`高度塌陷的问题`。什么是`高度塌陷`？

> 父元素没有加高度，高度自适应，子元素 float 后，造成父元素高度为0，称为高度塌陷问题。
>
> 会造成父级元素浮在上方，父级元素下方的元素顶上来。



------



## 2.定位：

> position: static; 可以清除定位，（是不受 上下左右 影响的）。
>
> position: relative; 绝对定位；
>
> position: absolute;相对定位
>
> position: fixed; 浮动定位；
>
> position: sticky; 的元素根据用户的滚动位置进行定位，粘性定位



## 3.边距（内外边距）

> margin: 0 0 0 0; // 外边距 调整相邻盒子的距离    四个参数 分别对应 上 右 下 左
>
> padding: 0 0 0 0; //内边距 主要作用是撑开盒子



## 4.伪类选择器部分：

### 4.1. 规定属于其父元素的第 * 个子元素的样式

```css
li:nth-child(1){}
```

### 2. 选择器匹配作为任何元素的第一个子元素的 <p> 元素：

```css
p:first-child{}
```

### 3. input 聚焦后的样式：

```css
input:invalid{}
```

### 4. 指定属于其父元素的最后一个子元素的 p 元素的样式

```css
p:last-child{} 
```



## 5.控制四个角变圆

```css
border-radius: 1px 1px 40px 40px;
```



## 6.让长列表网页的`渲染性能`提升

> https://web.dev/content-visibility/   参考

```css
content-visibility: auto;
```



## 7.阴影：

![syntax-1](http://www.webhek.com/wordpress/wp-content/uploads/2014/03/syntax-1.png)

```css
box-shadow:2px 2px 5px #000;
```

## 8.透明属性：

```css
opacity:0.4;
```

## 9.css设置字体：

```css
body,html{
    font-family:"宋体"
}
```

## 10.在一个盒子中 文本超出隐藏，超出部分显示 `...`



```css
.issue{
		width: 280upx;
		height: 60upx;
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap; 
	}
```






