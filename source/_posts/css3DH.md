---
    title: css3
    date: 2021-06-29 #发布时间
    categories: css #分类
    tags: css  #标签
---



# `CSS3` 边框

- border-radius 
- box-shadow
- border-image

## 1. border-radius 边框圆角：

```html
div { border:2px solid #a1a1a1; width:300px; height:100px; border-radius:25px;}

<div>border-radius 属性允许您为元素添加圆角边框！ </div>
```

## 2. box-shadow 元素阴影：

```html
div{width:300px;height:100px;	background-color:yellow;box-shadow: 10px 10px 5px #888888;}

<div></div>
```

## 3. border-image 边框图片：

```
#round{border-image:url(border.png) 30 30 round; width:250px;padding:10px 20px;}
<div id="round">这里，图像平铺（重复）来填充该区域。</div>
```



# `CSS3 border-radius` - 指定每个圆角

如果你在 border-radius 属性中只指定一个值，那么将生成 4 个 圆角。

但是，如果你要在四个角上一一指定，可以使用以下规则：

> - **四个值:** 第一个值为左上角，第二个值为右上角，第三个值为右下角，第四个值为左下角。
> - **三个值:** 第一个值为左上角, 第二个值为右上角和左下角，第三个值为右下角
> - **两个值:** 第一个值为左上角与右下角，第二个值为右上角与左下角
> - **一个值：**四个圆角值相同

```
border-radius: 15px 50px 30px 5px:
```



问题：**border-radius:50% 和 100% 的区别**  ？？？发现 border-radius:50% 和 border-radius:100% 的效果是相同的

> 其实在 W3C 中，如果两个相邻角的半径之和超过了相应盒子边的长度，那么浏览器要重新计算，以保证两者不会重合。
>
> 假设有一个 100px 的盒子，若 border-top-left-radius:100%; 则盒子会变成一个半径为 100px 的 1/4圆。（如下图左）
>
> 这个时候，如果我们再给一个 border-top-right-radius:100%; 此时相邻的两个角的半径之和已经超过了盒子的长度，浏览器需要重新计算。计算的规则就是同时缩放两个圆角的半径，直至两个相邻角的半径和为盒子的长度。也就是说，当两个圆角的半径为 **50%** 的时候，圆角正好符合 W3C 标准。（下图右）

![](https://www.runoob.com/wp-content/uploads/2021/03/1044766-20170103164726159-1801632772.png)



------





# CSS3 背景

> - background-image
> - background-size
> - background-origin
> - background-clip

## 1.background-image:背景图片：

```css
#example1 { 
    background-image: url(img_flwr.gif), url(paper.gif); 
    background-position: right bottom, left top; 
    background-repeat: no-repeat, repeat; 
}
```

## 2.CSS3 background-size 属性：

background-size指定背景图像的大小。CSS3以前，背景图像大小由图像的实际大小决定。

```css
div
{
    background:url(img_flwr.gif);
    background-size:80px 60px;
    background-repeat:no-repeat;
}
```

## 3.CSS3 的 background-origin 属性

background-origin 属性指定了背景图像的位置区域。

content-box, padding-box,和 border-box区域内可以放置背景图像。 

![](https://www.runoob.com/images/background-origin.gif)

```css
div
{
    background:url(img_flwr.gif);
    background-repeat:no-repeat;
    background-size:100% 100%;
    background-origin:content-box;
}
```





------



# CSS3 渐变（Gradients）

CSS3 定义了两种类型的渐变（gradients）：

> - **线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向**
> - **径向渐变（Radial Gradients）- 由它们的中心定义**

## 1.CSS3 线性渐变

为了创建一个线性渐变，你必须至少定义两种颜色节点。颜色节点即你想要呈现平稳过渡的颜色。同时，你也可以设置一个起点和一个方向（或一个角度）。

**线性渐变 - 从上到下（默认情况下）**

```css
#grad {
    background-image: linear-gradient(#e66465, #9198e5);
}
```

**线性渐变 - 从左到右**

```css
#grad {
  height: 200px;
  background-image: linear-gradient(to right, red , yellow);
}
```

**线性渐变 - 对角**

```css
#grad {
  height: 200px;
  background-image: linear-gradient(to bottom right, red, yellow);
}
```

## 2.CSS3 径向渐变

径向渐变由它的中心定义。

![](https://www.runoob.com/wp-content/uploads/2014/07/gradient_radial.jpg)



```css
#grad {
  background-image: radial-gradient(red, yellow, green);
}
```



------



# 设置文本效果（跳过）



# 设置字体（跳过）





------



# CSS3 2D 转换

## 2D 转换

> - translate()
> - rotate()
> - scale()
> - skew()
> - matrix()

## 1.translate()方法

> ranslate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。
>
> translate值（50px，100px）是从左边元素移动50个像素，并从顶部移动100像素。

![](https://www.runoob.com/images/transform_translate.gif)

```css
div
{
transform: translate(50px,100px);
-ms-transform: translate(50px,100px); /* IE 9 */
-webkit-transform: translate(50px,100px); /* Safari and Chrome */
}
```



## 2.rotate()

> otate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。
>
> rotate值（30deg）元素顺时针旋转30度。

![](https://www.runoob.com/images/transform_rotate.gif)

```css
div
{
transform: rotate(30deg);
-ms-transform: rotate(30deg); /* IE 9 */
-webkit-transform: rotate(30deg); /* Safari and Chrome */
}
```



## 3.scale() 方法：

> scale() 方法用于增加或缩小元素的大小。
>
> scale（2,3）转变宽度为原来的大小的2倍，和其原始大小3倍的高度。

![](https://www.runoob.com/images/transform_scale.gif)

```css
transform: scale(2,3); /* 标准语法 *
```



## 4.skew() 方法:

> 包含两个参数值，分别表示`X`轴和`Y`轴倾斜的角度，
>
> 如果第二个参数为空，则默认为0，参数为负表示向相反方向倾斜。
>
> - skewX(<angle>);表示只在X轴(水平方向)倾斜。
> - skewY(<angle>);表示只在Y轴(垂直方向)倾斜。

skew(30deg,20deg) 元素在X轴和Y轴上倾斜20度30度。

```css
div{transform: skew(30deg,20deg);}
```



## 5.matrix() 方法:

> matrix()方法和2D变换方法合并成一个。
>
> matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。

![](https://www.runoob.com/images/transform_rotate.gif)

利用matrix()方法旋转div元素30°

```css
div{transform:matrix(0.866,0.5,-0.5,0.866,0,0);}
```



## 6.介绍一下 deg 单位：CSS3 角度单位 deg(度)；

> 使用说明
>
> **度（Degress）。一个圆共360度**
>
> 90deg = 100grad = 0.25turn ≈ 1.570796326794897rad



------



# CSS3 3D 转换

> - rotateX()
> - rotateY()



## 1.rotateX() 方法:

> rotateX()方法，围绕其在一个给定度数X轴旋转的元素。

```css
div{ transform: rotateX(120deg);}
```

![](https://www.runoob.com/images/transform_rotatex.gif)



## 2.rotateY() 方法:

> rotateY()方法，围绕其在一个给定度数Y轴旋转的元素。

```css
div{ transform: rotateY(130deg);}
```

![](https://www.runoob.com/images/transform_rotatey.gif)



------



# CSS3 过渡



> CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。
>
> 要实现这一点，必须规定两项内容：
>
> - 指定要添加效果的CSS属性   **
> - 指定效果的持续时间。 **
> - **注意：** 如果未指定的期限，transition将没有任何效果，因为默认值是0。

一个典型CSS属性的变化是用户鼠标放在一个元素上时：下面是一个两秒变长的一个过度效果

```css
div
{
	width:100px;
	height:100px;
	background:red;
	transition:width 2s;
	-webkit-transition:width 2s; /* Safari */
}

div:hover
{
	width:300px;
}

<div></div>
```

注：当然过度效果还有其他的属性包括 多长事件触发、过渡效果（快慢）、渡效果何时开始、等等。。





# `css3`动画：在一个元素上加动画：

> @keyframes 规则是创建动画。 
>
> @keyframes 规则内指定一个 CSS 样式和动画将逐步从目前的样式更改为新的样式。



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



| [@keyframes](https://www.runoob.com/cssref/css3-pr-animation-keyframes.html) | 规定动画。                                                   |      |
| ------------------------------------------------------------ | :----------------------------------------------------------- | ---- |
| [animation](https://www.runoob.com/cssref/css3-pr-animation.html) | 所有动画属性的简写属性。                                     |      |
| [animation-name](https://www.runoob.com/cssref/css3-pr-animation-name.html) | 规定 @keyframes 动画的名称。                                 |      |
| [animation-duration](https://www.runoob.com/cssref/css3-pr-animation-duration.html) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。             |      |
| [animation-timing-function](https://www.runoob.com/cssref/css3-pr-animation-timing-function.html) | 规定动画的速度曲线。默认是 "ease"。                          |      |
| [animation-fill-mode](https://www.runoob.com/cssref/css3-pr-animation-fill-mode.html) | 规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式。 |      |
| [animation-delay](https://www.runoob.com/cssref/css3-pr-animation-delay.html) | 规定动画何时开始。默认是 0。                                 |      |
| [animation-iteration-count](https://www.runoob.com/cssref/css3-pr-animation-iteration-count.html) | 规定动画被播放的次数。默认是 1。                             |      |
| [animation-direction](https://www.runoob.com/cssref/css3-pr-animation-direction.html) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。          |      |
| [animation-play-state](https://www.runoob.com/cssref/css3-pr-animation-play-state.html) | 规定动画是否正在运行或暂停。默认是 "running"。               |      |



------



# CSS3 多列（跳过）

> 个人感觉有点不实用



------



# CSS3 用户界面（跳过）

> 暂且也跳过



------



# CSS 图片（跳过）

> 暂且跳过  可以去看看 css3图片中的响应式图片、图片滤镜、图片点击模态框、还是很强大的，稍后在补充吧。（时间有限）



------



# css3按钮（跳过）

> 可以去看看css3 的按钮：鼠标悬停按钮、按钮阴影、禁用按钮、按钮动画（波纹效果、按压效果）、都很奈斯（稍后补充）



------



# css3 分页

> 简单介绍包括：
>
> 1. 普通的分页
> 2. 面包屑

## 1.分页 ：

![](..\images\fy.jpg)

## 2.面包屑：

![](..\images\mbx.jpg)



------



# css3 框大小

> CSS3 `box-sizing` 属性可以设置 width 和 height 属性中包含了 padding(内边距) 和 border(边框)。 
>
> box-sizing 的作用是什么？？？看完下面的演示就知道了

## 1.不使用 CSS3 box-sizing 属性



> 以下两个 <div> 元素虽然宽度与高度设置一样，但真实展示的大小不一致，因为 div2 指定了内边距:

```css
.div1 {
    width: 300px;
    height: 100px;
    border: 1px solid blue;
}
.div2 {
    width: 300px;
    height: 100px;
    padding: 50px;
    border: 1px solid red;
} 
```



![](..\images\box-1.jpg)

## 2.使用 CSS3 box-sizing 属性



```css
.div1 {
    width: 300px;
    height: 100px;
    border: 1px solid blue;
    box-sizing: border-box;
}
div2 {
    width: 300px;
    height: 100px;
    padding: 50px;
    border: 1px solid red;
    box-sizing: border-box;
} 
```

> 可以看见下面红色块不会受到`padding`而影响到`div`的宽高,只会改变内容的边距

![](..\images\box-2.jpg)



------



# css3 媒体查询

> 媒体查询可用于检测很多事情，例如：
>
> - viewport(视窗) 的宽度与高度
> - 设备的宽度与高度
> - 朝向 (智能手机横屏，竖屏) 。
> - 分辨率

## CSS3 多媒体类型

| 值     | 描述                             |
| ------ | -------------------------------- |
| all    | 用于所有多媒体类型设备           |
| print  | 用于打印机                       |
| screen | 用于电脑屏幕，平板，智能手机等。 |
| speech | 用于屏幕阅读器                   |



## 首先使用媒体查询 要先设置meta标签

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```

这段代码的几个参数解释：

- **width = device-width：**宽度等于当前设备的宽度
- **initial-scale：**初始的缩放比例（默认设置为1.0）  
- **minimum-scale：**允许用户缩放到的最小比例（默认设置为1.0）  
- **maximum-scale：**允许用户缩放到的最大比例（默认设置为1.0）  
- **user-scalable：**用户是否可以手动缩放（默认设置为no，因为我们不希望用户放大缩小页面） 

## 使用

可以看到 @media screen and (max-width: 900px) 这段的意思是 当设备宽度到达或者小于900像素，将改变 test 的样式

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

