---
    title: css-flex-弹性盒子
    date: 2021-06-29 #发布时间
    categories: css #分类
    tags: css  #标签
---


# 弹性盒子flex

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

