---
title: CSS基础
date: 2016-01-29 13:32:09
tags: css
categories: 前端
---

#### 1.CSS 背景

    颜色 background-color         rgba/十六进制/red
    图片 background-image         url("img.png")
    重复 background-repeat        no-repeat/repeat-x
    滚动 background-attachment    scroll/fixed
    定位 background-position      left top/0 0/50% 50%
    尺寸 background-size           |contain;
    定位 background-origin        padding-box|border-box|content-box;
    区域 background-clip          border-box|padding-box|content-box;

<!-- more -->

#### 2.CSS 文本格式

    文本颜色    color	
    文本方向    direction	          ltr/rtl
    字符间距    letter-spacing	
    文本行高    line-height	        数字乘字体尺寸来设置行间距
    文本对齐    text-align	         justify/left/right/center
    文本修饰    text-decoration	    underline/overline/line-through/blink
    首行缩进    text-indent	        
    文本阴影    text-shadow	        h-shadow v-shadow blur color
    控制字母    text-transform	     capitalize/uppercase/lowercase
    文本重写    unicode-bidi	       bidi-override
    垂直对齐    vertical-align	     sub/super/top/middle/bottom
    空白处理    white-space	        pre/nowrap/pre-wrap/pre-line
    汉字间距    word-spacing	
    text-overflow   ellipsis
    word-wrap   break-word  指定如果足够长得话，应该换行：
    word-break  break-all	允许在单词内换行。

#### 3.CSS 字体

    文本字体 font "font-style font-variant font-weight font-size/line-height font-family"
    文本字体系列 font-family	
    文本字体大小 font-size	
    文本字体样式 font-style	 italic/oblique
    以小型大写字体或者正常字体显示文本 font-variant	
    字体粗细 font-weight normal 400/blod 500
    @font-face 规则
    @font-face{
        font-family: myFirstFont;
        src: url(sansation_light.woff);
    } 
    div{font-family:myFirstFont;}

#### 4.CSS 链接

    a:link {color:#000000;}      /* 未访问链接*/
    a:visited {color:#00FF00;}  /* 已访问链接 */
    a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
    a:active {color:#0000FF;}  /* 鼠标点击时 */

#### 5.CSS 列表

    列表项标记浏览器兼容性解决方案
    ul{
        list-style-type: none;
        padding: 0px;
        margin: 0px;
    }
    ul li{
        background-image: url(sqpurple.gif);
        background-repeat: no-repeat;
        background-position: 0px 5px; 
        padding-left: 14px; 
    }

    list-style	简写属性。用于把所有用于列表的属性设置于一个声明中
    list-style-image	将图象设置为列表项标志。
    list-style-position	设置列表中列表项标志的位置。
    list-style-type	设置列表项标志的类型。

#### 6.CSS 盒子模型

    width浏览器的兼容性问题
    根据 W3C 的规范，元素内容占据的空间是由 width 属性设置的，
    而内容周围的 padding 和 border 值是另外计算的。
    不幸的是，IE5.X 和 6 在怪异模式中使用自己的非标准模型。
    这些浏览器的 width 属性不是内容的宽度，
    而是内容、内边距和边框的宽度的总和。
    ···
    解决方式
    不要给元素添加具有指定宽度的内边距，
    而是尝试将内边距或外边距添加到元素的父元素和子元素。

    浏览器的兼容性问题
    IE8 及更早IE版本不支持 填充的宽度和边框的宽度属性设。
    ···
    解决方式
    解决IE8及更早版本不兼容问题可以在HTML页面声明 <!DOCTYPE html>即可。

#### 7.CSS 边框

    边框样式    border-style dotted 点线/dashed 虚线/solid 实线
    圆角 border-radius
    盒阴影 box-shadow "h-shadow v-shadow blur spread color inset"
    边界图片 border-image "source slice width outset repeat"

#### 8.CSS 轮廓

    outline

#### 9.CSS Display(显示) 与Visibility（可见性）

    Display
    none	此元素不会被显示。
    block	此元素将显示为块级元素，此元素前后会带有换行符。
    inline	默认。此元素会被显示为内联元素，元素前后没有换行符。
    inline-block 行内块元素
    ...
    Visibility
    hidden 隐藏但是空间被占据

#### 10.CSS Positioning(定位)

    static  默认值，即没有定位，在文档流中
    relative    相对其正常位置。
    fixed   相对于浏览器窗口是固定位置。
    absolute    相对于最近的已定位父元素或者html

px:Fixed 定位在 IE7 和 IE8 下需要描述 !DOCTYPE 才能支持.
#### 11.CSS Float(浮动)
    一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
    浮动元素之后的元素将围绕它。

    left    元素向左浮动。
    right   元素向右浮动。

    px:clear 清除浮动
#### 12.CSS clip 属性
    裁剪一张图像：
    img 
    {
    position:absolute;
    clip:rect(0px,60px,200px,0px);
    }
#### 13.CSS 水平对齐(Horizontal Align)

    在IE8中使用margin:auto属性无法正常工作，除非声明 !DOCTYPE

    IE5中块元素有一个margin处理BUG。在IE5中，需要添加一些额外的代码
    .container{text-align:center;}
    .center{
    margin-left:auto;
    margin-right:auto;
    width:70%;
    background-color:#b0e0e6;
    text-align:left;}

    IE8和早期有一个问题，当使用position属性时。
    如果一个容器元素（在本例中<div class="container">）指定的宽度，
    !DOCTYPE声明是缺失，IE8和早期版本会在右边增添17px的margin。
    这似乎是一个滚动的预留空间。
    使用position属性时始终设置在DOCTYPE声明中！

    IE8和早期有一个问题，当使用position属性时。
    如果一个容器元素（在本例中<div class="container">）指定的宽度，
    !DOCTYPE声明是缺失，IE8和早期版本会在右边增添17px的margin。
    这似乎是一个滚动的预留空间。
    使用position属性时始终设置在DOCTYPE声明中！
    float同样如此。

#### 14.CSS 组合选择符

    后代选取器(以空格分隔)
    子元素选择器(以大于号分隔）
    相邻兄弟选择器（以加号分隔）
    普通兄弟选择器（以破折号分隔）
    :first-child 伪类来选择元素的第一个子元素
    q:lang(no) {quotes: "~" "~";} 注意: 仅当 !DOCTYPE 已经声明时 IE8 支持 :lang.

#### 15.CSS 图像透明/不透明

    opacity:0.4;
    filter:alpha(opacity=40); /* IE8 及其更早版本 */

#### 16.CSS 媒体类型

    @media 规则
    @media 规则允许在相同样式表为不同媒体设置不同的样式。

#### 17.CSS 属性 选择器
    注意：IE7和IE8需声明!DOCTYPE才支持属性选择器！IE6和更低的版本不支持属性选择器。
#### 18.CSS3 渐变（Gradients）

    background: linear-gradient(direction, color-stop1, color-stop2, ...);
    background: linear-gradient(angle, color-stop1, color-stop2);
    background: radial-gradient(center, shape size, start-color, ..., last-color)

#### 19.CSS3 2D 转换
    transform 
    translate(50px,100px) 
    rotate(30deg)
    scale(2,3)
    skew(30deg,20deg)
    matrix()
    
#### 20.CSS3 3D 转换
    transform 
    transform-style:preserve-3d;显示3D
    perspective 透视距离
    backface-visibility	定义元素在不面对屏幕时是否可见。
#### 21.CSS3 过渡

    transition: property duration timing-function delay;

#### 22.CSS3 动画

    @keyframes 规则
    @keyframes myfirst{
        from {background: red;}
        to {background: yellow;}
    }
    div
    {
        animation-name: myfirst;
        animation-duration: 5s;
        animation-timing-function: linear;
        animation-delay: 2s;
        animation-iteration-count: infinite;
        animation-direction: alternate;
        animation-play-state: running;
    }
    animation: name duration timing-function delay 
                iteration-count direction fill-mode play-state;

#### 23.CSS3 box-sizing
    border-box; 则 padding(内边距) 和 border(边框) 也包含在 width 和 height 中

#### 24.CSS3 弹性盒子(Flex Box)
    弹性盒子内容
    display: -webkit-flex;
    flex-direction: row：横向从左到右排列（左对齐），默认的排列方式。
                    row-reverse：反转横向排列（右对齐，从后往前排，最后一项排在最前面。
                    column：纵向排列。
                    column-reverse：反转纵向排列，从后往前排，最后一项排在最上面。
    justify-content: flex-start | flex-end | center | space-between | space-around
    align-items: flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
                 flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
                 center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
                 baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
                 stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
    flex-wrap: nowrap - 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。
               wrap - 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行
               wrap-reverse -反转 wrap 排列。
    align-content: stretch - 默认。各行将会伸展以占用剩余的空间。
                   flex-start - 各行向弹性盒容器的起始位置堆叠。
                   flex-end - 各行向弹性盒容器的结束位置堆叠。
                   center -各行向弹性盒容器的中间位置堆叠。
                   space-between -各行在弹性盒容器中平均分布。
                   space-around - 各行在弹性盒容器中平均分布，两端保留子元素与子元素之间间距大小的一半。
    弹性子元素属性
    order: <integer>：用整数值来定义排列顺序，数值小的排在前面。可以为负值。
    完美的居中:
    .flex-item {
      margin: auto;
    }
    align-self: auto：如果'align-self'的值为'auto'，则其计算值为元素的父元素的'align-items'值，如果其没有父元素，则计算值为'stretch'。
                flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
                flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
                center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
                baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
                stretch：如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制。
    flex: auto: 计算值为 1 1 auto
          initial: 计算值为 0 1 auto
          none：计算值为 0 0 auto
          inherit：从父元素继承
          [ flex-grow ]：定义弹性盒子元素的扩展比率。
          [ flex-shrink ]：定义弹性盒子元素的收缩比率。
          [ flex-basis ]：定义弹性盒子元素的默认基准值。