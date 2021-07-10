---
title: css练习（持续更新）
date: 2021-07-10
categories: css
tags: css练习实践  #标签
---


# jq点击按钮触发css3动画

> 其实很简单，没有想象的那么复杂，实现方法主要是向`#aaa`添加动画属性

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
          transition: width 2s;
        }
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

