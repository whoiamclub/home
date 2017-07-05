---
title: form对象
date: 2017-07-02 13:32:00
tags: [html]
categories: 前端
description: 数据交互与dom操作并列前端两大基石
---

&lt;form&gt; 标签用于为用户输入创建 HTML 表单。
表单能够包含 input 元素，比如文本字段、复选框、单选框、提交按钮等等。
表单还可以包含 menus、textarea、fieldset、legend 和 label 元素。
表单用于向服务器传输数据。
<!--more-->
## 例子
``` bash
<form action="url" enctype="multipart/form-data" name="form1" target="_blank" method="get" >
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>
```

## form元素属性
<table class="table table-bordered table-striped table-condensed"><tr><th>属性</th><th>值</th><th>描述</th></tr><tr><td>accept-charset</td><td>charset_list</td><td>规定服务器可处理的表单数据字符集。</td></tr><tr><td>action</td><td>URL</td><td>规定当提交表单时向何处发送表单数据。</td></tr><tr><td rowspan="2">autocomplete</td><td>on</td><td rowspan="2">规定是否启用表单的自动完成功能。</td></tr><tr><td>off</td></tr><tr><td rowspan="2">method</td><td>get</td><td rowspan="2">规定用于发送 form-data 的 HTTP 方法。</td></tr><tr><td>post</td></tr><tr><td>name</td><td>form_name</td><td>规定表单的名称。</td></tr><tr><td rowspan="5">target</td><td>_blank</td><td rowspan="5">规定在何处打开 action URL。</td></tr><tr><td>_self</td></tr><tr><td>_parent</td></tr><tr><td>_top</td></tr><tr><td>framename</td></tr><tr><td rowspan="3">enctype</td><td>application/x-www-form-urlencoded</td><td rowspan="3"></td></tr><tr><td>multipart/form-data</td></tr><tr><td>text/plain</td></tr></table>

## Form 对象
Form 对象代表一个 HTML 表单。
在 HTML 文档中&lt;form&gt; 每出现一次，Form 对象就会被创建。

## Form 对象属性

<table class="table table-bordered table-striped table-condensed"><tr><th>属性</th><th>描述</th></tr><tr><td>acceptCharset</td><td>服务器可接受的字符集。</td></tr><tr><td>action</td><td>设置或返回表单的 action 属性。</td></tr><tr><td>enctype</td><td>设置或返回表单用来编码内容的 MIME 类型。</td></tr><tr><td>id</td><td>设置或返回表单的 id。</td></tr><tr><td>length</td><td>返回表单中的元素数目。</td></tr><tr><td>method</td><td>设置或返回将数据发送到服务器的 HTTP 方法。</td></tr><tr><td>name</td><td>设置或返回表单的名称。</td></tr><tr><td>target </td><td>设置或返回表单提交结果的 Frame 或 Window 名。</td></tr></table>

## Form 对象方法/句柄
submit()	提交表单。
onsubmit	在提交表单之前调用。
