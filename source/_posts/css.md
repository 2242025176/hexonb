---
    title: css常用
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

> ###### position: static; 可以清除定位，（是不受 上下左右 影响的）。
>
> ###### position: relative; 绝对定位；
>
> ###### position: absolute;相对定位
>
> ###### position: fixed; 浮动定位；
>
> position: sticky; 的元素根据用户的滚动位置进行定位，粘性定位



## 3.边距（内外边距）

> margin: 0 0 0 0; // 外边距 调整相邻盒子的距离    四个参数 分别对应 上 右 下 左
>
> padding: 0 0 0 0; //内边距 主要作用是撑开盒子



## 4.伪类选择器部分：

### 1. 规定属于其父元素的第 * 个子元素的样式

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

## 10.css 媒体查询：

```css
.test{
			width: 500px;
			height: 400px;
			background-color: red;
		}
@media screen and (max-width: 900px){
			.test{
				width: 100%;
				height:200px;
				background-color:blue;
			}
		}
```

## 11.在一个盒子中 文本超出隐藏，超出部分显示 `...`



```css
.issue{
		width: 280upx;
		height: 60upx;
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap; 
	}
```





------





# 二、移动端弹性盒子flex

## 1.`flex`它的所有子元素自动成为容器成员

```css
display: flex;
```

`行内元素`也可以使用Flex布局。

```css
display: inline-flex;
```

## 2.容器的属性

### 2.1 flex-direction属性：属性决定主轴的方向（即项目的排列方向）。

```css
flex-direction: row | row-reverse | column | column-reverse;
```

![img](https://www.runoob.com/wp-content/uploads/2015/07/0cbe5f8268121114e87d0546e53cda6e.png)

> - row（默认值）：主轴为水平方向，起点在`左端`。
> - row-reverse：主轴为水平方向，起点在`右端`。
> - column：主轴为垂直方向，起点在`上沿`。
> - column-reverse：主轴为垂直方向，起点在`下沿`。

### 2.2 flex-wrap属性  : （`换行属性`）

默认情况下，项目都排在一条线（又称”轴线”）上。

flex-wrap属性定义，如果一条轴线排不下，如何`换行`。

![img](https://www.runoob.com/wp-content/uploads/2015/07/903d5b7df55779c03f2687a7d4d6bcea.png)

```css
flex-wrap: nowrap | wrap | wrap-reverse;
```

> （1）nowrap（默认）：不换行。
>
> （2）wrap：换行，第一行在上方。
>
> （3）wrap-reverse：换行，第一行在下方。

### 2.3 flex-flow：

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

```css
.box {
  flex-flow: <flex-direction> <flex-wrap>;
}
```

### 2.4 justify-content属性：属性定义了项目在主轴上的对齐方式（`水平对齐`）

```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

> - flex-start（默认值）：左对齐
> - flex-end：右对齐
> - center： 居中
> - space-between：两端对齐，项目之间的间隔都相等。
> - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### 2.5 align-items属性:属性定义项目在交叉轴上如何对齐(`垂直对齐`)

```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

> - flex-start：交叉轴的起点对齐。
> - flex-end：交叉轴的终点对齐。
> - center：交叉轴的中点对齐。
> - baseline: 项目的第一行文字的基线对齐。
> - stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。







------



# 三、`css3`动画：在一个元素上加动画：

列子：在以下div中加动画效果

```html
<div class="xin"> </div>
```

##### 1.使用简写属性把 animation 绑定到一个`<div>` 元素：

```css
.xin{
    width: 100px;
    height: 100px;
    background-color: brown;
    animation: xin 1s infinite; /* 指定@keyframes规则多少秒执行完成 */
}
```

##### 2.使用 `@keyframes`规则，你可以创建动画。0％是开头动画，100％是当动画完成。

```css
 @keyframes xin {
     0% {
         transform:translate(-50%, -50%) scale(1)rotate(45deg);
     }
     50% {
         transform:translate(-50%, -50%) scale(1.1)rotate(45deg);
     }
     100% {
         transform:translate(-50%, -50%) scale(1)rotate(45deg);
     }
  }
```

2. 属性定义是否应该轮流反向播放动画。

```css
animation-direction:alternate; 
```

##### 





------
