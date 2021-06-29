---
    title: css3动画
    date: 2021-06-29 #发布时间
    categories: css #分类
    tags: css  #标签
---

# `css3`动画：在一个元素上加动画：

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



