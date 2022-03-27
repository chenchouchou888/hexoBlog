---
title: CSS面试
tags: CSS
---

##水平垂直居中方法
###行内元素
lineheight + text-align

###块级元素
###flex:
```bash
justify-content + align-items
```
```bash
margin:auto
```


###子绝父相 : 
```bash
left top 50% + transform： translate(-50%,-50%)
```
```bash
left top 50% margin-left,margin-top 50%自身宽高
```
```bash
四项0 margin:auto
```

###table-cell + inline-block 
```bash
vertical-align (不设inline-block也可以垂直居中)  text-align (需要设置inline-block)
```

####以上除了依赖margin的 都不需要具体宽高就可以实现

##BFC（块级格式上下文）
####BFC的概念

BFC是一个独立的渲染区域，规定了内部box如何布局， 并且这个区域的子元素不会影响到外面的元素，其中比较重要的布局规则有内部 box 垂直放置，计算 BFC 的高度的时候，浮动元素也参与计算。
BFC的原理布局规则

内部的Box会在垂直方向，一个接一个地放置
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反
BFC的区域不会与float box重叠
BFC是一个独立容器，容器里面的子元素不会影响到外面的元素
计算BFC的高度时，浮动元素也参与计算高度
元素的类型和display属性，决定了这个Box的类型。不同类型的Box会参与不同的Formatting Context。

####如何创建BFC？

根元素，即HTML元素
float的值不为none
position为absolute或fixed
display的值为inline-block、table-cell、table-caption
overflow的值不为visible

####BFC的使用场景

去除边距重叠现象
清除浮动（让父元素的高度包含子浮动元素）
避免某元素被浮动元素覆盖
避免多列布局由于宽度计算四舍五入而自动换行
