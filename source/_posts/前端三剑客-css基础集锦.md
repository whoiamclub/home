---
title: 前端三剑客-css基础集锦
date: 2017-07-01 10:21:44
tags: [css,初级]
categories: 前端面试圣经初级
---
css是页面展示及特效最直接表现的语言，前端开发除了要了解每个css属性的表现外，更要注重每个属性在不同浏览器之间差异，并完美的解决。
<!-- more -->
#### 1.CSS 背景

background:背景占据元素的所有内容区域，包括 padding 和 border，但是不包括元素的 margin。它在 Firefox, Safari ,Opera 以及 IE8 中工作正常，但是 IE6 和 IE7 中，background 没把 border 计算在内。
 
    //指定填充背景的颜色
    //设置背景颜色之外，如果元素底层的背景图不可用，还可以设置一个“回退色”。
    //通过在回退色之前增加一个斜杠(/)来实现。
    background-color         rgba|#000000|red| green / blue
    
    //引用图片作为背景
    //路径是相对于样式所处文件的
    background-image         url("img.png")
    
    //决定是否重复背景图片
    //CSS2中当图片平铺时，会被元素在末端截断。CSS3 引入了两个属性来修正这个问题:
    //space: 应用同等数量的空白到图片之间，直到填满整个元素 
    //round: 缩小图片直到正好平铺满元素 
    background-repeat        no-repeat|repeat-x
    
    //决定背景图是否随页面滚动。
    //当设置 background-attachment 为 fixed 时，
    //当页面向下滚动时，背景要待在它原来的位置(相对于浏览器来说)。
    //也就是不随元素滚动。只能出现在它父元素能达到的区域。
    //background-attachment :local; 背景图会随内容的滚动而滚动。
    background-attachment    scroll|fixed
    
    //指定元素背景图片的位置
    background-position      left top|0 0|50% 50%
    
    //尺寸 
    background-size          cover|contain;
    
    //背景原点
    //可以从边框，内补白或者内容盒子开始计算 background-position。
    background-origin        padding-box|border-box|content-box;
    
    //背景修剪
    //background-clip:text结合text-fill-color制作文字渐变效果
    h1{font-size:60px;
      background: linear-gradient(to bottom,#FCF,#000);
      -webkit-background-clip:text;
      -webkit-text-fill-color:transparent;
    }
    background-clip          border-box|padding-box|content-box;
    
    //新增属性background-break
    background-break: continuous; 
    默认值。忽略盒之间的距离(也就是像元素没有分成多个盒子，依然是一个整体一样) 
    background-break: bounding-box; 
    把盒之间的距离计算在内
    background-break: each-box; 
    为每个盒子单独重绘背景
技巧：

仿栏：当使用 css 的 float 属性来定位布局元素时，要确保两栏或多栏有相同的长度是比较困难的。如果长度不同，其中一栏的背景会比另外的短，这会破坏整个设计。
思路很简单：不再给每列单独设置背景，而是给各列的父元素设置一个背景图。所有栏的设计都包含在这张图片之中。

文本替换：一个适用于任意浏览器的简单方法是，用想用的字体来做一张文本图片，并用这张图片作为背景。这样，文本依然出现在文档标记中以供搜索引擎检索和屏幕浏览器识别，但是在浏览器中就会显示首选的字体。
>{background:url(text.jpg) 0 0 no-repeat; text-indent: -9999px;}


#### 2.CSS 文本格式

    文本颜色    color	
    文本方向    direction	          ltr/rtl
    文本对齐    text-align	         justify/left/right/center
    文本修饰    text-decoration	    underline/overline/line-through/blink
    控制字母    text-transform	     capitalize/uppercase/lowercase
    文本重写    unicode-bidi	       bidi-override
    汉字间距    word-spacing	
    字符间距    letter-spacing	
    
     //text-stroke + text-fill-color制作文字镂空效果
     h1{
         font-size:60px;
         -webkit-text-fill-color:transparent;
         -webkit-text-stroke:1px #fff;
     }
     text-stroke 文字描边;
     text-fill-color 文字填充色
    
    //首行缩进
    //不影响元素的宽度，适用于block层级的元素；
    //ie input缩进有兼容问题。使用padding-left来代替，需要对宽度重新设置。 
    text-indent	  
    
    //文本阴影
    //全兼容写法
    //-webkit-transform:translate(2px, 20px);
    //-moz-text-shadow:0 0 10px #C06;
    //-webkit-text-shadow:0 0 10px #c06;
    //text-shadow:0 0 10px #c06;
    //filter: Shadow(Color='green', Direction='135', Strength='6')/*Direction阴影的方向*/
    //filter: dropshadow(OffX=2, OffY=2, Color='black', Positive='true');
    text-shadow	        h-shadow v-shadow blur color
    
    //文本行高
    //撑开inline高度的不是文字，而是line-height；
    //使用行高垂直居中
    //使用行高代替高度避免haslayout
    line-height	        数字乘字体尺寸来设置行间距
        
    //垂直对齐    
      vertical-align: baseline;sub;super;text-top;text-bottom;middle;bottom;top;
      /* <长度> 值 */
      vertical-align: 10em;4px;
      /* <百分比> 值 */
      vertical-align: 10%;
      {line-height: 30px;vertical-align: -10%;}
      实际上，等同于：{line-height: 30px;vertical-align: -3px;/* = 30px * -10% */  }
      /* 全局值 */
      vertical-align: inherit;initial;unset;
   
    //解决图片下边缘留空隙是由vertical-align和line-height造成的。
    //解决方法
    1.让vertical-align失效，设置display:block;
    2.vertical-align:bottom/middle/top;
    3.line-height小于字体大小;
    4.font-size:0
    //绝对居中div>img
    div { line-height: 240px; font-size: 0; }
    img { vertical-align: middle; }
    //重点：一个inline-block元素，如果里面没有inline内联元素，或者overflow不是visible，
    //则该元素的基线就是其margin底边缘，否则，其基线就是元素里面最后一行内联元素的基线。
       
    
    //处理换行、空格和Tab
    /normal（浏览器默认值），即换行符无效、多个空格及Tab被折叠成一个空格来处理、文本内容会自动换行。
    //nowrap，文本内容不自动换行，换行符无效、多个空格及Tab被折叠成一个空格来处理。
    //pre，换行符有效、多个空格及Tab不会被折叠，文本不会自动换行。可以保留其中的换行及缩进。
    //pre-wrap，换行符有效、多个空格及Tab不会被折叠、文本内容会自动换行
    //pre-line，换行符有效、多个空格及Tab被折叠成一个空格来处理、文本内容会自动换行
    //<pre>的浏览器默认样式中就有white-space: pre;。
    white-space	        pre/nowrap/pre-wrap/pre-line
    
    //溢出文本显示省略号
    //display: inline-block;text-overflow:ellipsis;overflow:hidden;white-space:nowrap;
    text-overflow   ellipsis
    
    //一个长单词超出整个容器宽度时是否换行
    word-wrap   break-word  指定如果足够长得话，应该换行：
    
    //决定文本的换行点
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

    Css盒模型magin外边距+border边框+padding内边距+width内容
    当设置background颜色的时候，会覆盖border+padding+width;

    width浏览器的兼容性问题
    根据 W3C 的规范，元素内容占据的空间是由 width 属性设置的，
    w3c中的盒子模型的宽仅包括content;
    而内容周围的 padding 和 border 值是另外计算的。
    不幸的是，IE5.X 和 6 在怪异模式中使用自己的非标准模型。
    这些浏览器的 width 属性不是内容的宽度，
    而是内容、内边距和边框的宽度的总和。
    ie怪异盒模型的宽包括border*2+padding*2+content;
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

    边框样式border-style dotted 点线/dashed 虚线/solid 实线
    
    圆角border-radius
    盒阴影 box-shadow "h-shadow v-shadow blur spread color inset"
    //全兼容
    box {
      -moz-border-radius: 15px; /* Firefox */
      -webkit-border-radius: 15px; /* Safari 和 Chrome */
      border-radius: 15px; /* Opera 10.5+, 以及使用了IE-CSS3的IE浏览器 */
    
      -moz-box-shadow: 10px 10px 20px #000; /* Firefox */
      -webkit-box-shadow: 10px 10px 20px #000; /* Safari 和 Chrome */
      box-shadow: 10px 10px 20px #000; /* Opera 10.5+, 以及使用了IE-CSS3的IE浏览器 */
    
      behavior: url(ie-css3.htc); /* 通知IE浏览器调用脚本作用于'box'类 */
    }
    
    边界图片 border-image "source slice width outset repeat"
[ie-css3.htc](/js/ie-css3.htc)
#### 8.CSS 轮廓

    outline

#### 9.CSS Display(显示) 与Visibility（可见性）

Display

    none	此元素不会被显示。
    //隐藏元素并脱离文档流
    
    block	此元素将显示为块级元素，此元素前后会带有换行符。
    //不设置宽度时，宽度为父元素宽度，不设置高度时，高度为零或者子元素的行高。
      独占一行
      支持宽高
    //不支持  vertical-align
    
    inline	默认。此元素会被显示为内联元素，元素前后没有换行符。
    //内容撑开宽度
      非独占一行
      不支持宽高
      代码换行被解析成空格
    //不支持
    //background-position
      clear
      clip
      height | max-height | min-height
      width | max-width | min-width
      overflow
      text-align
      text-indent
      text-overflow
      
    inline-block 行内块元素
    //不设置宽度时，内容撑开宽度
      非独占一行
      支持宽高
      代码换行被解析成空格
    //不支持clear
    //IE兼容
      IE7-浏览器不支持给块级元素设置inline-block样式，解决方法如下：首先将其变成行内元素，使用具有行内元素的特性，然后触发haslayout，使其具有块级元素的特性，如此就可以模拟出inline-block的效果
      div{display:inline-block;*display: inline;zoom: 1;}

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
float浮动： 
1、块在一排显示（使块元素在一排显示）
2、内联支持宽高（使内联元素支持设置高度）
3、默认内容撑开宽度（没有宽度自动撑开）前几个与inline-block效果相同
4、脱离文档流（浮动元素有可能会覆盖正常文档流中内容）
5、提升层级半层（浮动会挤开元素内的内容）

left    元素向左浮动。
right   元素向右浮动。

//bug如果父类包含一个浮动元素，浮动元素并不会撑开父类
IE浏览器不兼容浮动float的解决办法。
一、并排两个div：ie或者ff下对于子div设置float:left的，另外的子div没有设置float-left的话，两个浏览器下会有区别，具体有一个会产生间隙。兼容做法就是都设置float属性。但是记住有设置过float就要将float clear掉，不然下面的div会叠在已float的div上。通常把清除浮动写成单独的<div class=”clear”></div>放在所有浮动div的最下方。
二、在上述1情况中需要设置子div的宽度，假如不设置的话子div的宽度会被默认为父div的100%，这样float根本就产生不了效果。当然还可以用display:inline的方法让两个子div并排,但是这样的话div的宽度设置将会失效(要把子div撑大只能靠里面的元素)。
三、ie中父div被设置成特定高度之后，假如里面的浮动子div高度超过了母div设置的高度,ie会自动把母div撑大，但是ff却不能，ff中父div的高度会依然，里面的子层会溢出到外面来。兼容方法：不要设置父级高度。

#### 12.CSS clip 属性
    裁剪一张图像：
    img {
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
    
    //全兼容写法
    .gradient{
        background: #000000;
        background: -moz-linear-gradient(top,  #000000 0%, #ffffff 100%);
        background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#000000), color-stop(100%,#ffffff));
        background: -webkit-linear-gradient(top,  #000000 0%,#ffffff 100%);
        background: -o-linear-gradient(top,  #000000 0%,#ffffff 100%);
        background: -ms-linear-gradient(top,  #000000 0%,#ffffff 100%);
        background: linear-gradient(to bottom,  #000000 0%,#ffffff 100%);
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000000', endColorstr='#ffffff',GradientType=0 );
    }
    :root .gradient{filter:none;}

#### 19.CSS3 2D 转换
    //transform 
    transform: rotate(30deg);
    -ms-transform: rotate(30deg); /* IE 9 */
    -webkit-transform: rotate(30deg); /* Safari and Chrome */
    
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
    
    -moz-box-sizing: content-box;
    -webkit-box-sizing: content-box;
    -o-box-sizing: content-box;
    -ms-box-sizing: content-box;
    box-sizing: content-box; 
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
          
    兼容写法
    .box{
        display: -webkit-flex;  /* 新版本语法: Chrome 21+ */
        display: flex;          /* 新版本语法: Opera 12.1, Firefox 22+ */
        display: -webkit-box;   /* 老版本语法: Safari, iOS, Android browser, older WebKit browsers. */
        display: -moz-box;      /* 老版本语法: Firefox (buggy) */
        display: -ms-flexbox;   /* 混合版本语法: IE 10 */   
    }
    .flex1 {            
        -webkit-flex: 1;        /* Chrome */  
        -ms-flex: 1             /* IE 10 */  
        flex: 1;                /* NEW, Spec - Opera 12.1, Firefox 20+ */
        -webkit-box-flex: 1     /* OLD - iOS 6-, Safari 3.1-6 */  
        -moz-box-flex: 1;       /* OLD - Firefox 19- */       
    }