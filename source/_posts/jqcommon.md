---
title: jquery常用语法
date: 2021-06-27
categories: jquery #分类
tags: jquery  #标签
---


# jq 部分：

基本的选择器:

```js
$("#id")            //ID选择器
$("div")            //元素选择器
$(".classname")     //类选择器
$(".classname,.classname1,#id1")     //组合选择器
```



## 1、jq的.css属性：设置多个css属性:

```javascript
$("p").css({"background-color":"yellow","font-size":"200%"});
```

## 2、ajax 请求：

原文链接：https://blog.csdn.net/jinixin/article/details/80042763

```js
$.ajax({
    url: "/greet",
    data: {name: 'jenny'},
    type: "POST",
    dataType: "json",
    success: function(data) {
        // data = jQuery.parseJSON(data);  //dataType指明了返回数据为json类型，故不需要再反序列化
      
    }
});
```

## 3、初始化加载：

```js
$(document).ready(function(){
	trace("初始化方法进入");
});
------------------------------
$(function(){
    ...
})
```

## 4、jq事件：

#### 4.1 鼠标事件：

> 1. `click()`：点击事件 
> 2. `dblclick()` ：双击事件
> 3. `mouseenter()`：鼠标移入
> 4. `mouseleave()`：鼠标移出
> 5. `hover()` : 鼠标移入移出

```js
//click
$("p").click(function(){
   alert("段落被点击了。");
  });
---------------------------------
//双击事件
$("p").dblclick (function(){
   alert("段落被双击击了。");
  });
------------------------------------
//鼠标移入事件
$("p").mouseenter(function(){
    $("p").css("background-color","yellow");
  });
---------------------------------------
//鼠标移出事件
("p").mouseleave(function(){
    $("p").css("background-color","lightgray");
  });
------------------------------------------
//hover 
 $("p").hover(function(){
    $("p").css("background-color","yellow");
    },function(){
    $("p").css("background-color","pink");
  });
```

#### 

#### 4.2 表单事件：

> 1. change() 事件：change 事件会在元素失去焦点时触发
> 2. focus() 聚焦事件
> 3. blur() : 当元素失去焦点时发生 blur 事件。

```js
 // change 事件
$("input").change(function(){
    alert("文本已被修改");
});
// 聚焦
$("input").focus(function(){
    $("span").css("display","inline").fadeOut(2000);
 });
//失焦
$("input").blur(function(){
    alert("输入框失去了焦点");
  });

```

#### 4.3 文档/窗口 事件：

> 1. resize() 事件。当调整浏览器窗口大小时触发
> 2. scroll()  事件。当用户滚动指定的元素时，会触发 scroll 事件。

```js
// 当调整浏览器窗口大小时，发生 resize 事件。
$(window).resize(function(){
    $("span").text(x+=1);
  });
//scroll() 滚动监听事件。
$("div").scroll(function(){
    $("span").text(x+=1);
});
```



## 5、jq遍历方法：

> $.each() 方法 遍历数组  ：（`es6` 的` for ... of` 方法也可以实现）

```js
data: [{id: 1, title: "博客/ HBase技术社区", pic: "No.1 - 时序数据库随笔 - InfluxDB&Flux调试环境搭建", desc: "喜欢 #数据库",…},…] 
//以上是要遍历的数组数据
$.each(data,function(arr,res){
         console.log(res)//会循环出 数组下的所有对象           
 })
```



## 6、渲染页面的方法：

> 1. append() 方法在被选元素的结尾插入指定内容。
> 2. html() 方法设置或返回被选元素的内容（innerHTML）。

```js
$("#btn1").click(function(){
    $("p").append(" <b>插入文本</b>.");
});
$("#btn2").click(function(){
    $("ol").append("<li>插入项</li>");
});

//html 方法 改变所有 <p> 元素的内容：
$("button").click(function(){
		$("p").html("Hello <b>world!</b>");
});
```

