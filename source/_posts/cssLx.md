---
title: css练习（持续更新）
date: 2021-07-10
categories: css
tags: css练习实践  #标签
---


# jq点击按钮触发css3动画

> 其实很简单，没有想象的那么复杂，实现方法主要是向`#aaa`添加动画属性。

<!-- more --> 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #aaa {
          width: 100px;
          height: 100px;
          background: blue;
          /* transition: width 2s; 过度动画 */
        }
        /* 使用@keyframes规则，你可以创建动画。 */
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
      </style>
</head>
<body>
    <button onclick="big()">开始</button>
    <button onclick="small()">关闭</button>
    <div id="aaa"></div>
</body>
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>
    function big() {
      $("#aaa").css({"animation":"xin 1s infinite"});
    }
    function small() {
      $("#aaa").css({"animation":"xin 0s infinite"});
    }
  </script>
</html>
```

> 为了更明了的阅读这里解读css3的语法
>
> transform属性应用于元素的`2D或3D`转换。这个属性允许你将元素旋转，缩放，移动，倾斜等。
>
> scale() 定义 2D 缩放转换。
>
> rotate() 定义 2D 旋转，在参数中规定角度。
>
> deg单位在css3文章中有介绍：**度（Degress）。一个圆共360度**