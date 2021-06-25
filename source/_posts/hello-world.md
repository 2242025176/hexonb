---
title: 常用语法
categories: 科普总结 #分类
tags: 常用  #标签
---

# 常用的各种语法：

## 一、css常用的方法和选择器用法：

### css最基本的语法：

#### 1.浮动：

```css
float:right;/* left  right  none*/
```

清除浮动的方法：（不止以下两种方法）

> 1. 给父级加高
> 2. 父级使用overflow: hidden;属性

不清除浮动会造成`高度塌陷的问题`。什么是`高度塌陷`？

> 父元素高度自适应，子元素 float 后，造成父元素高度为0，称为高度塌陷问题。
>
> 会造成父级元素浮在上方，父级元素下方的元素顶上来。

### 2.定位：

> #### position: static; 可以清除定位，（是不受 上下左右 影响的）。
>
> #### position: relative; 绝对定位；
>
> #### position: absolute;相对定位
>
> #### position: fixed; 浮动定位；
>
> #### position: sticky; 的元素根据用户的滚动位置进行定位，粘性定位

### 3.边距（内外边距）

> margin: 0 0 0 0; // 外边距 调整相邻盒子的距离    四个参数 分别对应 上 右 下 左
>
> padding: 0 0 0 0; //内边距 主要作用是撑开盒子

#### 伪类选择器部分：

1. 规定属于其父元素的第 * 个子元素的样式

   ```css
   li:nth-child(1){}
   ```

2. 选择器匹配作为任何元素的第一个子元素的 <p> 元素：

   ```css
   p:first-child{}
   ```

3. input 聚焦后的样式：

   ```css
   input:invalid{}
   ```

4. 指定属于其父元素的最后一个子元素的 p 元素的样式

   ```css
   p:last-child{} 
   ```

5. 控制四个角变圆

   ```css
   border-radius: 1px 1px 40px 40px;
   ```

6. 让长列表网页的`渲染性能`提升

   ```css
   content-visibility: auto;
   ```

### 常用的语法部分：

#### 1.阴影：

![syntax-1](http://www.webhek.com/wordpress/wp-content/uploads/2014/03/syntax-1.png)

```css
box-shadow:2px 2px 5px #000;
```

#### 2.透明属性：

```css
opacity:0.4;
```

#### 3.css设置字体：

```css
body,html{
    font-family:"宋体"
}
```

#### 4.html title 设置小logo：

> 在 <head>下引入以下

```html
<link rel="icon" type="image/x-icon" href="./img/logo.jpg"/>
```

#### 5.css 媒体查询：

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

### 6.在一个盒子中 文本超出隐藏，超出部分显示 `...`



```css
.issue{
		width: 280upx;
		height: 60upx;
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap; 
	}
```

### 7. css中auto作用是？

> auto是自适应的意思，auto是很多尺寸值的默认值，也就是由浏览器自动计算。
>
> 块级元素中margin、border、padding以及content宽度之和构成父元素width。
>
> 使用auto属性后，父元素宽度发生变化，该元素的宽度也会随之变化。



# 二、弹性盒子常用:

## 1.flex它的所有子元素自动成为容器成员

```css
display: flex;
```

行内元素也可以使用Flex布局。

```css
display: inline-flex;
```

## 2容器的属性

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



# 三、css3动画：在一个元素上加动画：

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

##### 2.使用 @keyframes规则，你可以创建动画。0％是开头动画，100％是当动画完成。

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


# 四、less 部分：

## 问题：less在普通html运行会报 跨域问题 :

> #### 解决方法:在服务器环境下使用；可以用node搭建web服务；或者在 hbuliderx 上打开运行 就可以解决；



# 五、js部分：



**1、三目运算：**(布尔表达式 ? 值0:值1;)

```js
5 > 3 ? alert('5大') : alert('3大');

即  if(5>3){alert('5大')}else{alert('3大')};	
```

##### 2、回调函数：（想要在另一个 构造函数 内拿到 参数 必须通过回调函数的形式）

```javascript
function fn(res){
        //回调函数的解析
        // var res = function(data){console.log(data)}
        setTimeout(() => {  //计时器 异步处理函数 
            var data = 'hello'
            res(data)  		//res 对应的 fn构造函数方法的 返回值
        }, 1000);
    }
    //如果要获取一个函数中的异步结果，则必须通过 回调函数 获取
    fn((data)=>{
        console.log(data) //获取计时器 里面的参数
    })
```

## 3.常用的遍历方法：

### 3.1 for循环：

```js
var arrd = ['1','2','3'];
 for(var i = 0;i<arrd.length ;i++){
        console.log(arrd[i]) //1 2 3
 }
```

### 3.2 for...in 语句

**for...in 语句用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。**

```js
var arrd = ['1','2','3'];
var person = {fname:"John", lname:"Doe", age:25};
for(var x in person){
    console.log(person[x])// John Doe 25
}
```

### 3.3 forEach:

- 按照索引的顺序按个传递给定义的一个函数，并且可以在原数组的基础上进行修改

```js
 var arrd = ['1','2','3'];
 arrd.forEach(function(x,i,a){
   console.log( a[i] = x + 1 ) // 11 21 31
 }) ;
// 其中调用函数中有三个参数，x 表示数组中元素，i 表示下标，a 表示数组本身
```

### 3.4 map :

- 将调用的数组的每个元素传递给指定的函数，并`返回一个新数组`，且函数必须有返回值

```js
var arr=[1,2,3]; 
var list = arr.map(function(x){ 
        return x + x; 
 });
 console.log(list) //[2, 4, 6]
```

### 3.5 for-of :

参考：https://blog.csdn.net/w390058785/article/details/80522383

ES6中，新增了for-of遍历方法。它被设计用来遍历`各种类数组集合`，例如DOM NodeList对象、Map和Set对象，甚至字符串也行。

使用例子（一）遍历数组里的每一项。

```js
var arr = ['nick','freddy','mike','james'];
for(var item of arr){	
    console.log(item);
    // 输出结果：nick
     //       freddy
      //      mike
        //    james
}
```

使用例子（二）

```js

var arr = [
    { name:'nick', age:18 },
    { name:'freddy', age:24 },
    { name:'mike', age:26 },
    { name:'james', age:34 }
];
for(var item of arr){	
    console.log(item.name,item.age); //nick 18 、freddy 24  ...以下省略
}
```

### 3.6 filter() 过滤：

```js
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x > 2;
});
console.log(r) //[4, 5, 6, 9, 10, 15] 过滤掉小于 2 的数字
```

### 3.7 while 循环 (`javascript`中不常用的判断循环) **补充** **

只要指定条件为 `true`，循环就可以一直执行代码块。

实例：

```js
while (i<5)
{
    x=x + "The number is " + i + "<br>";
    i++;
}

```



## 4. 面向对象封装：注：（结合 5、6、观看）

以我之前的canvas小案例为例：

```js
//获取画布
    var canvas = document.getElementById('mycanvas');
    //获取上下文
    var ctx = canvas.getContext('2d');
    //封装 canvas 方法
    function Rect(x,y,w,h,color) { //构造函数
        //维护状态
        this.x = x;
        this.y = y;
        this.w = w;
        this.h = h;
        this.color = color;
    }
    //更新的方法 
    Rect.prototype.update = function() {
        this.x++;
    };
    //渲染
    Rect.prototype.render = function () {
        //设置颜色：
        ctx.fillStyle = this.color;
        //渲染
        ctx.fillRect(this.x,this.y,this.w,this.h);
    };
    //实例
    var R1 = new Rect(100,100,50,50,'purple')
    var R2 = new Rect(100,300,100,100,'blue')
    //动画过程：
    setInterval(() => {
        //清除
        ctx.clearRect(0,0,canvas.width,canvas.height);
        //R1更新 调用 方法
        R1.update();
        //R1渲染
        R1.render();
        //R2更新
        R2.update();
        //R2渲染
        R2.render();
    }, 10);
```



## 5.构造函数是指什么？

> 所谓"构造函数"，其实就是一个普通函数，但是内部使用了[`this`变量](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)。
>
> 对构造函数使用`new`运算符，就能生成实例，并且`this`变量会绑定在实例对象上。

例子：

摘自 阮一峰-面向对象教程

```js
function Cat(name,color){

　　　　this.name=name;

　　　　this.color=color;

　　}
//我们现在就可以生成实例对象了。
　　var cat1 = new Cat("大毛","黄色");

　　var cat2 = new Cat("二毛","黑色");

　　alert(cat1.name); // 大毛

　　alert(cat1.color); // 黄色
```

构造函数方法很好用，但是存在一个浪费内存的问题。(这里就不多举例了-去阮一峰看)

## 6. **Prototype模式**（继承）

> - Javascript规定，每一个构造函数都有一个`prototype`属性，指向另一个对象。
> - 这个对象的所有属性和方法，都会被构造函数的实例继承。
>
> 这意味着，我们可以把那些不变的属性和方法，直接定义在`prototype`对象上。

例子：

```js
　　function Cat(name,color){

　　　　this.name = name;

　　　　this.color = color;

　　}

　　Cat.prototype.type = "猫科动物";

　　Cat.prototype.eat = function(){alert("吃老鼠")};
//然后，生成实例。
　　var cat1 = new Cat("大毛","黄色");

　　var cat2 = new Cat("二毛","黑色");

　　alert(cat1.type); // 猫科动物

　　cat1.eat(); // 吃老鼠
```

## 7. new 到底起到什么作用：

> 众所周知，在JS中，new的作用是通过构造函数来创建一个实例对象。
>
> # new操作符到底干了什么？
>
> 1. 创建一个新对象；
> 2. 将构造函数的作用域赋给新对象（因此this就指向了这个新对象）；
> 3. 执行构造函数中的代码（为这个新对象添加属性）；
> 4. 返回新对象；

## 8.数学函数 `Math` 常用方法

1.`Math.abs()` 获取绝对值 ：

```js
Math.abs(-12)   // 12
```

2.取整：`Math.ceil()  && Math.floor()` 向上取整和向下取整

```js
Math.ceil(10)  //=> 10
Math.ceil(10.01)  // =>11
Math.ceil(-10.01)  //=>-10
Math.floor(10.999)  //=> 10 
Math.floor(-10.099)  //=> -11
```

3.`Math.round()` 四舍五入 ：
注意：正数时，包含5是向上取整，负数时包含5是向下取整。

```js
Math.round(-16.3) = -16
Math.round(-16.5) = -16
Math.round(-16.51) = -17
```

4.* 随机数: （parseInt 取整数）

案例1：获取`[0,10]`的随机整数

```js
console.log(parseInt(Math.random()*10)); //未包含10
console.log(parseInt(Math.random()*10+1)); //包含10
```

案例2：获取[n,m]之间的随机整数

```js
Math.round(Math.random()*(m-n)+n)
```

5.圆周率 PI ：绘制圆（canvas 中 会用到）

```js
Math.PI  // = 3.141592654
```



## 9.常用时间函数 `new Date()`

1.获取当前时间

```js
var mydate=new Date(); // (中国标准时间)
```

2.获取时间常用方法

```js

mydate.getFullYear(); //获取完整的年份(4位,1970-???) result：2018
mydate.getMonth(); //获取当前月份(0-11,0代表1月) result：9
mydate.getDate(); //获取当前日(1-31) result：23
mydate.getDay(); //获取当前星期X(0-6,0代表星期天) result：2
mydate.getHours(); //获取当前小时数(0-23) result：10
mydate.getMinutes(); //获取当前分钟数(0-59) result：18
mydate.getSeconds(); //获取当前秒数(0-59) result：45
mydate.getTime(); //获取当前时间(从1970.1.1开始的毫秒数) result：1540261028601
mydate.toLocaleDateString(); //获取当前日期 result：2018/10/23
mydate.toLocaleTimeString(); //获取当前时间 result：上午10:13:26
mydate.toLocaleString( ); //获取日期与时间 result：2018/10/23 上午10:14:21

parse() //方法可解析一个日期时间字符串，并返回 1970/1/1 午夜距离该日期时间的毫秒数。
replace() //方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。
```

3.补充 % 取余 ，疑问 % 这个东东 ，起到了什么作用？

> %操作符是求余数，保留整数的意思，这个是取余运算，不是除法运算。
>
> 一共有三种情况（够除有余数、不够除、没有余数。）
>
> 够除有余数：案例：12除以5=2，余数是2，即5*2+2=12，所以12%5=2*



## 9.定时器有以下两个方法：

- `setInterval() `：按照指定的周期（以毫秒计）来调用函数或计算表达式。方法会不停地调用函数，直到 `clearInterval()` 被调用或窗口被关闭。
- `setTimeout() `：在指定的毫秒数后调用函数或计算表达式。

持续调用，一般写，时钟 会用到这种方法

```js
function lets (){
    console.log('持续执行');
}
setInterval(lets,1000)
```

`setTimeout` 只会执行一次

```js
setTimeout(console.log('执行一次'),1000)
```



## 10.转换字符串的方法

1、`toString()`方法

`toString()`方法返回的是相应值的字符串表现

数值、布尔值、对象和字符串值都有`toString()`方法，但是null和undefined值没有这个方法

```js
var age = 11;
var str1 = age.toString();              //字符串 “11”

var found = true;
var str2 = found.toString();           //字符串 “true”
```

## 11. 判断方法 `Switch` 语句

> 使用 `switch` 语句来选择`多个需被执行的代码`块之一。
>
> 注 ：多个条件判断 可以使用这个方法

案例1：

> `case `判断 与 `switch(d) `中返回的参数 是否对等？

```js
var d=new Date().getDay(); 
switch (d) 
{ 
  case 0:x="今天是星期日"; 
  break; 
  case 1:x="今天是星期一"; 
  break; 
  case 2:x="今天是星期二"; 
  break; 
  case 3:x="今天是星期三"; 
  break; 
  case 4:x="今天是星期四"; 
  break; 
  case 5:x="今天是星期五"; 
  break; 
  case 6:x="今天是星期六"; 
  break; 
}
```

案例2：

> `default`  是 规定`匹配不存在时`做的事情：

```js
var d=new Date().getDay();
switch (d)
{
    case 6:x="今天是星期六";
    break;
    case 0:x="今天是星期日";
    break;
    default:
    x="期待周末";
}
document.getElementById("demo").innerHTML=x;
```

## 

## 12.今天遇到一个问题 indexOf is undefind；

此错误是 数组为空 ；附上判断数组的方法

```js
let arr = [];
if (arr.length == 0){
   console.log("数组为空")
}else {
   console.log("数组不为空")
}
```


