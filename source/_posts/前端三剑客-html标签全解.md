---
title: 前端三剑客-html标签全解
date: 2017-06-30 22:36:39
tags: [html,初级]
categories: 前端面试圣经初级
---

html标签是前端界面的骨架，作为一个前端开发我们对每个标签的熟悉程度就应该如同骨科医生对人体每一块骨头的熟知，哪怕他在不常见。
<!-- more -->
#### 文档标签
&lt;!DOCTYPE&gt; 	定义文档类型。

    1.HTML 5
    <!DOCTYPE html>
    2.HTML 4.01 Strict
    该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
    3.HTML 4.01 Transitional
    该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
    "http://www.w3.org/TR/html4/loose.dtd">
    4.HTML 4.01 Frameset
    该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
    "http://www.w3.org/TR/html4/frameset.dtd">
    5.XHTML 1.0 Strict
    该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    6.XHTML 1.0 Transitional
    该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。必须以格式正确的 XML 来编写标记。
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "
    http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    7.XHTML 1.0 Frameset
    该 DTD 等同于 XHTML 1.0 Transitional，但允许框架集内容。
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" 
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
    8.XHTML 1.1
    该 DTD 等同于 XHTML 1.0 Strict，但允许添加模型（例如提供对东亚语系的 ruby 支持）。
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
&lt;html&gt;	定义 HTML 文档。
&lt;head&gt;	定义关于文档的信息。
&lt;meta&gt;	定义关于 HTML 文档的元信息。
&lt;title&gt;	定义文档的标题。
&lt;link&gt;	定义文档与外部资源的关系。
&lt;style&gt;	定义文档的样式信息。
&lt;script&gt;	定义客户端脚本。
&lt;noscript&gt;	定义针对不支持客户端脚本的用户的替代内容。
&lt;body&gt;	定义文档的主体。
&lt;base&gt;	定义页面中所有链接的默认地址或默认目标。

    <base> 标签为页面上的所有链接规定默认地址或默认目标。
    通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。
    使用 <base> 标签可以改变这一点。浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。这其中包括 <a>、<img>、<link>、<form> 标签中的 URL。
    <base> 标签必须位于 head 元素内部。
&lt;div&gt;	定义文档中的节。
&lt;span&gt;	定义文档中的节。

#### 语义标签
&lt;nav&gt;	定义导航链接。
&lt;main&gt;  规定文档的主要内容
&lt;header&gt;	定义 section 或 page 的页眉。  
&lt;section&gt;	定义 section。
&lt;article&gt;	定义文章。

    <article> 标签规定独立的自包含内容。
    一篇文章应有其自身的意义，应该有可能独立于站点的其余部分对其进行分发。
    <article> 元素的潜在来源：论坛帖子|报纸文章|博客条目|用户评论 
&lt;aside&gt;	定义页面内容之外的内容。
    
    <aside> 的内容可用作文章的侧栏。
&lt;footer&gt;	定义 section 或 page 的页脚。
&lt;address&gt;	定义文档作者或拥有者的联系信息。

    <address> 标签定义文档或文章的作者/拥有者的联系信息。
    如果 <address> 元素位于 <body> 元素内，则它表示文档联系信息。
    如果 <address> 元素位于 <article> 元素内，则它表示文章的联系信息。
    <address> 元素中的文本通常呈现为斜体。大多数浏览器会在 address 元素前后添加折行。


#### 短语元素标签  
&lt;cite&gt;	定义引用(citation)。   
&lt;code&gt;	定义计算机代码文本。
&lt;em&gt;	定义强调文本。
&lt;dfn&gt;	定义定义项目。
&lt;strong&gt;	定义强调文本。
&lt;samp&gt;	定义计算机代码样本。
&lt;kbd&gt;	定义键盘文本。
&lt;var&gt;	定义文本的变量部分。

    以上元素都是短语元素。虽然这些标签定义的文本大多会呈现出特殊的样式，但实际上，这些标签都拥有确切的语义。
    我们并不反对使用它们，但是如果您只是为了达到某种视觉效果而使用这些标签的话，我们建议您使用样式表，那么做会达到更加丰富的效果。
#### 文本类标签
&lt;b&gt;	定义粗体字。
&lt;small&gt;	定义小号文本。
&lt;i&gt;	定义斜体字。
&lt;del&gt;	定义被删除文本。
&lt;ins&gt;	定义被插入文本。   

    <del>定义文档中已被删除的文本。
    <ins> 标签定义已经被插入文档中的文本。
&lt;sub&gt;	定义下标文本。
&lt;sup&gt;	定义上标文本。
&lt;p&gt;	定义段落。
&lt;pre&gt;	定义预格式文本。
&lt;h1&gt; to &lt;h6&gt;	定义 HTML 标题。
&lt;hr&gt;	定义水平线。
&lt;br&gt;	定义简单的折行。
&lt;big&gt;	定义大号文本。
&lt;bdi&gt;	定义文本的文本方向，使其脱离其周围文本的方向设置。
    
    目前只有 Firefox 和 Chrome 支持 <bdi> 标签。
    bdi 指的是 bidi 隔离。
    <bdi> 标签允许您设置一段文本，使其脱离其父元素的文本方向设置。
    在发布用户评论或其他您无法完全控制的内容时，该标签很有用。
    属性dir：ltr|rtl
&lt;bdo&gt;	定义文字方向。

    所有浏览器都支持 <bdo> 标签。
    bdo 元素可覆盖默认的文本方向

#### 表格元素标签
&lt;table&gt;	定义表格。
&lt;caption&gt;	定义表格标题。

    caption 元素定义表格标题。
    caption 标签必须紧随 table 标签之后。您只能对每个表格定义一个标题。通常这个标题会被居中于表格之上。
&lt;thead&gt;	定义表格中的表头内容。
&lt;tbody&gt;	定义表格中的主体内容。
&lt;tr&gt;	定义表格中的行。
&lt;th&gt;	定义表格中的表头单元格。
&lt;td&gt;	定义表格中的单元。
&lt;colgroup&gt;	定义表格中供格式化的列组。
&lt;col&gt;	定义表格中一个或多个列的属性值。
    
    <col> 标签为表格中一个或多个列定义属性值。可以对全部列应用样式。
    只能在 table 或 colgroup 元素中使用 <col> 标签。
    水平align：right|left|center|justify|cha
    垂直valign：top|middle|bottom|baseline
    charoff：规定第一个对齐字符的偏移量。
    span：规定 col 元素应该横跨的列数。
&lt;tfoot&gt;	定义表格中的表注内容（脚注）。

#### 列表元素标签
&lt;ul&gt;	定义无序列表。
&lt;ol&gt;	定义有序列表。
&lt;li&gt;	定义列表的项目。
&lt;dl&gt;	定义定义列表。
&lt;dd&gt;	定义定义列表中项目的描述。
&lt;dt&gt;	定义定义列表中的项目。
    
    <dl>
       <dt>计算机</dt>
       <dd>用来计算的仪器 ... ...</dd>
    </dl>

#### 表单元素标签
&lt;form&gt;	定义供用户输入的 HTML 表单。
&lt;input&gt;	定义输入控件。

    根据不同的 type 属性值，输入字段拥有很多种形式。输入字段可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等等。
    type:button|checkbox|file|hidden|image|password|radio|reset|submit|text
&lt;label&gt;	定义 input 元素的标注。
    
    <label> 标签为 input 元素定义标注（标记）。
    label 元素不会向用户呈现任何特殊效果。不过，它为鼠标用户改进了可用性。如果您在 label 元素内点击文本，就会触发此控件。就是说，当用户选择该标签时，浏览器就会自动将焦点转到和标签相关的表单控件上。
    <label> 标签的 for 属性应当与相关元素的 id 属性相同。
&lt;textarea&gt;	定义多行的文本输入控件。
&lt;select&gt;	定义选择列表（下拉列表）。
&lt;optgroup&gt;	定义选择列表中相关选项的组合。
    
    <optgroup> 标签定义选项组。
    optgroup 元素用于组合选项。当您使用一个长的选项列表时，对相关的选项进行组合会使处理更加容易。
&lt;option&gt;	定义选择列表中的选项。
    
    option 元素定义下拉列表中的一个选项（一个条目）。
    浏览器将 <option> 标签中的内容作为 <select> 标签的菜单或是滚动列表中的一个元素显示。
    option 元素位于 select 元素内部。
&lt;fieldset&gt;	定义围绕表单中元素的边框。
&lt;legend&gt;	定义 fieldset 元素的标题。
    
    <form>
      <fieldset>
        <legend>health information</legend>
        height: <input type="text" />
        weight: <input type="text" />
      </fieldset>
    </form>
    fieldset 元素可将表单内的相关元素分组。
&lt;button&gt;	定义按钮 (push button)。
    
    <button> 标签定义一个按钮。在 button 元素内部，您可以放置内容，比如文本或图像。这是该元素与使用 input 元素创建的按钮之间的不同之处。
    如果在 HTML 表单中使用 button 元素，不同的浏览器会提交不同的值。
    Internet Explorer 将提交 <button> 与 <button/> 之间的文本，而其他浏览器将提交 value 属性的内容。
    请在 HTML 表单中使用 input 元素来创建按钮。

#### 工具类标签
&lt;canvas&gt;	定义图形。
&lt;audio&gt;	定义声音内容。

    属性	    值	        描述
    autoplay	autoplay	如果出现该属性，则音频在就绪后马上播放。
    controls	controls	如果出现该属性，则向用户显示控件，比如播放按钮。
    loop	    loop	    如果出现该属性，则每当音频结束时重新开始播放。
    muted	    muted	    规定视频输出应该被静音。
    preload 	preload	    如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。
    src     	url	        要播放的音频的 URL。

&lt;video&gt;	定义视频。
&lt;source&gt;

    <source> 标签为媒介元素（比如 <video> 和 <audio>）定义媒介资源。
    <source> 标签允许您规定可替换的视频/音频文件供浏览器根据它对媒体类型或者编解码器的支持进行选择。
&lt;embed&gt;	定义外部交互内容或插件。
&lt;map&gt;	定义图像映射。
&lt;area&gt;	定义图像映射内部的区域。

    1.area 元素永远嵌套在 map 元素内部。area 元素可定义图像映射中的区域。
    2.<img>中的 usemap 属性可引用 <map> 中的 id 或 name 属性（取决于浏览器），应同时向 <map> 添加 id 和 name 属性。
    3.area属性：shape	定义区域的形状。default|rect|circ|poly    
&lt;iframe&gt;	定义内联框架。
    
    longdesc	    URL	            规定一个页面，该页面包含了有关 iframe 的较长描述。
    name	        frame_name	    规定 iframe 的名称。
    sandbox	                        启用一系列对 <iframe> 中内容的额外限制。
    scrolling	    yes|no|auto     规定是否在 iframe 中显示滚动条。
    seamless	    seamless	    规定 <iframe> 看上去像是包含文档的一部分。
    src	            URL	            规定在 iframe 中显示的文档的 URL。
    srcdoc	        HTML_code	    规定在 <iframe> 中显示的页面的 HTML 内容。
    marginheight	pixels	        定义 iframe 的顶部和底部的边距。
    marginwidth	    pixels	        定义 iframe 的左侧和右侧的边距。
    frameborder	    1/0             规定是否显示框架周围的边框。    
    height	                        规定 iframe 的高度。
    width	                        定义 iframe 的宽度。


&lt;meter&gt;	定义预定义范围内的度量。
    
    <meter> 标签定义已知范围或分数值内的标量测量。也被称为 gauge（尺度）
    属性	    值	    描述
    form	    form_id	规定 <meter> 元素所属的一个或多个表单。
    high	    number	规定被视作高的值的范围。
    low 	    number	规定被视作低的值的范围。
    max	        number	规定范围的最大值。
    min	        number	规定范围的最小值。
    optimum	    number	规定度量的优化值。
    value	    number	必需。规定度量的当前值。
&lt;progress&gt;	定义任何类型的任务的进度。
    
    <progress> 标签标示任务的进度（进程）。
    max	    number	规定任务一共需要多少工作。
    value	number	规定已经完成多少任务。
&lt;img&gt;	定义图像。
&lt;a&gt;	定义锚。

    1.download 属性规定被下载的超链接目标。
    在 <a> 标签中必须设置 href 属性。
    该属性也可以设置一个值来规定下载文件的名称。所允许的值没有限制，浏览器将自动检测正确的文件扩展名并添加到文件 (.img, .pdf, .txt, .html, 等等)。
    2.target	规定在何处打开链接文档。
    值：_blank|_parent|_self|_top|framename
    3.type	规定被链接文档的的 MIME 类型。

#### 其他
&lt;!--...--&gt;	定义注释。
&lt;blockquote&gt;	定义长的引用。
&lt;q&gt; 标签定义短的引用。

    <blockquote> 与 </blockquote> 之间的所有文本都会从常规文本中分离出来，经常会在左、右两边进行缩进（增加外边距），而且有时会使用斜体。也就是说，块引用拥有它们自己的空间。
    <q>浏览器经常在引用的内容周围添加引号。
&lt;abbr&gt;	定义缩写。
    
    通过对缩写进行标记，您能够为浏览器、拼写检查和搜索引擎提供有用的信息。
    可以在 <abbr> 标签中使用全局的 title 属性，这样就能够在鼠标指针移动到 <abbr> 元素上时显示出简称/缩写的完整版本。
&lt;figcaption&gt;	定义 figure 元素的标题。
&lt;figure&gt;	定义媒介内容的分组，以及它们的标题。

    <figure> 标签规定独立的流内容（图像、图表、照片、代码等等）。
    figure 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响。