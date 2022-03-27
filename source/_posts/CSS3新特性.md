---
title: CSS3新特性
tags: CSS
---

###过渡    
transition： CSS属性，花费时间，效果曲线(默认ease)，延迟时间(默认0)复制代码

###动画
 animation：动画名称，一个周期花费时间，运动曲线（默认ease），动画延迟（默认0），播放次数（默认1），是否反向播放动画（默认normal），是否暂停动画（默认running）复制代码

###形状转换   
transform:适用于2D或3D转换的元素

rotate(30deg);   translate(30px,30px);   scale(.8);        skew(10deg,10deg);        rotateX(180deg);     rotateY(180deg);        rotate3d(10,10,10,90deg);

###选择器

###阴影    
box-shadow: 水平阴影的位置 垂直阴影的位置 模糊距离 阴影的大小 阴影的颜色 阴影开始方向（默认是从里往外，设置inset就是从外往里）;复制代码

###边框    
border-image: 图片url 图像边界向内偏移 图像边界的宽度(默认为边框的宽度) 用于指定在边框外部绘制偏移的量（默认0） 铺满方式--重复（repeat）、拉伸（stretch）或铺满（round）（默认：拉伸（stretch））;

###背景  

###反射 
 -webkit-box-reflect:方向[ above-上 | below-下 | right-右 | left-左 ]，偏移量，遮罩图片

###文字
 换行   语法：word-break: normal|break-all|keep-all;、语法：word-wrap: normal|break-word;  超出省略号   text-overflow:clip|ellipsis|string                                                                                                 文字阴影   语法：text-shadow:水平阴影，垂直阴影，模糊的距离，以及阴影的颜色。

###颜色  
rgba...

###Filter（滤镜）：
黑白色filter: grayscale(100%)、褐色filter:sepia(1)、饱和度saturate(2)、色相旋转hue-rotate(90deg)、反色filter:invert(1)、透明度opacity(.5)、亮度brightness(.5)、对比度contrast(2)、模糊blur(3px)

###弹性布局  Flex

###栅格布局 grid

###多列布局

###盒模型定义 

###媒体查询  @media

##详情
https://juejin.cn/post/6844903518520901639