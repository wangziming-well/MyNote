# HTML

HTML是用来描述网页的语言

* 指超文本标记语言
* ·
* HTML文档又称为网页

# 常用标签

## \<h>标题标签

~~~html
<h1>THis is a heading</h1> 
<h6>THis is a heading</h6>
~~~

## \<p>段落标签

~~~html
<p>This is a paragraph</p>
~~~

## \<a>超链接标签

~~~html
<a href = "https:\\www.baidu.com"> 百度</a>
~~~

## \<img>图像标签

~~~html
<img src = "test.png" width="300" height="512"/>
~~~

## 注释标签

~~~html
<!-- This is a comment -->
~~~

## \<hr />水平线标签

用于分隔内容

## \<br />换行标签

用于换行

## \<html>标签

定义了HTML文档

## \<head>头标签

 用来定义头部信息  主要用来封装其他位于文档头部的标记

## \<body> 体标签

定义页面要显示的内容，包括文字 ，图片 ，视频 ，音频等主要是展示给用户看的

## \<!DOCTYPE html>

告诉浏览器采用哪种编码类型  html5

## \<title>标题标签

记用于定义HTML页面的标题，即给网页取一个名字，必须位于\<head>标记之内。一个HTML文档只能含有一对\<title>\</title>标记，



# HTML元素

* 指从开始标签到结束标签的所有代码
* 元素可以是文本，也可以是标签

# 标签属性

* 标签可以拥有属性，为元素提供更多信息
* 属性以键值对的形式：`name="value"`
* 属性在HTML元素的开始标签中定义

* 适用于大部分标签的属性：

    | 属性  | 值                 | 描述                                     |
    | ----- | ------------------ | ---------------------------------------- |
    | class | *classname*        | 规定元素的类名（classname）              |
    | id    | *id*               | 规定元素的唯一 id                        |
    | style | *style_definition* | 规定元素的行内样式（inline style）       |
    | title | *text*             | 规定元素的额外信息（可在工具提示中显示） |

# HTML标题

* 通过\<h>标签定义
* HTML会自动在块级元素前后添加一个额外的空格，比如段落、标题
* 标题标签为HTML文档规划结构，可以帮助用户快速定位浏览

# HTML段落

* 通过\<p>标签定义

* HTML会忽略标签之前的文本排版（所有连续的空格或空行都会被算作一个空格）,所以要通过换行标签和段落标签来控制文本排版

# HTML样式

* 通过style属性改变HTMl元素的样式
* 会在CSS中具体学习

# HTML格式化

| 标签      | 描述                                        |
| :-------- | :------------------------------------------ |
| \<b>      | 定义粗体文本。                              |
| \<big>    | 定义大号字。                                |
| \<em>     | 定义着重文字。                              |
| \<i>      | 定义斜体字。                                |
| \<small>  | 定义小号字。                                |
| \<strong> | 定义加重语气。                              |
| \<sub>    | 定义下标字。                                |
| \<sup>    | 定义上标字。                                |
| \<ins>    | 定义插入字。（下划线）                      |
| \<del>    | 定义删除字。                                |
| \<s>      | *不赞成使用。*<br />使用 \<del> 代替。      |
| \<strike> | *不赞成使用。<br />*使用 \<del> 代替。      |
| \<u>      | *不赞成使用。*<br />使用样式（style）代替。 |

# HTML引用

* \<q>短引用

    <p>WWF 的目标是：<q>构建人与自然和谐共存的世界</q></p>

* \<blockquote>长引用

    <p>以下内容引用自 WWF 的网站：</p>
    <blockquote cite="http://www.worldwildlife.org/who/index.html">
    五十年来，WWF 一直致力于保护自然界的未来。
    世界领先的环保组织，WWF 工作于 100 个国家，
    并得到美国一百二十万会员及全球近五百万会员的支持。
    </blockquote>

* \<abbr>缩写标签

    <p><abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。</p>

# HTML超链接

* 通过\<a>标签创建链接：
* 两种使用\<a>标签的方式：
    * 通过href属性：创建指向另外一个文档的链接
    * 通过使用name属性-创建文档内的书签

* target属性：为`"_blank"`时点击链接会在新窗口打开文档

## 指向另一个文档

<a href="pathname">链接</a>



## 指向本文档的书签

* 创建书签：

<a name="label">书签（锚）</a>

* 指向书签的链接(在书签名前加#)：

<a href="#label">转到书签</a>

**提示**：假如浏览器找不到已定义的命名锚，那么就会定位到文档的顶端。不会有错误发生。

**显然可以直接指向其他文档的锚，只需要将#锚名添加到URL的末端**



# HTML图像

* 由\<img>标签定义
* 需要指定src属性，定位图像资源，以在网页上显示
* alt属性用来为图像定义一串预备的可替换文本
* 图像尺寸由width和height属性定义
* align属性
    * 设置图像浮动："left","right"
    * 设置图像在文本中的位置（上中下）:"bottom","middle","top"

# HTML表格

* \<table>标签表示整个表格
    * 属性 border控制边框
    * 属性cellpadding控制单元格边距
    * 属性cellsapcing控制单元格间距
    * 属性bgcolor控制表格背景颜色
    * 属性background控制表格背景图片
    * 属性width、height控制表格大小
    * 属性frame控制表格样式：box、above、below、hsides、vsides
* \<tr>标签表示表格的行
    * 定义属性colspan来跨列
* \<th>标签表示表格头
    * 可以作为单元格
* \<td>标签表示表格单元
    * 定义属性colspan来跨行
    * 属性bgcolor来控制单元格背景颜色
    * 属性background来控制单元格背景图片
    * 属性aligh控制单元格中内容的对齐方式left、right、center
* \<caption>标签标识表格的标题



# HTML列表

## 无序表

* 由\<ul>标签标识
    * 属性type控制无序表标志：disc、circle、square
* 列表项由\<li>定义



<ul type="circle">
    <li>Coffee</li>
    <li>Milk</li>
</ul>

## 有序表

* 由\<ol>标签标识
    * 属性type控制有序表标志：A,a,I,i
* 列表项\<li>定义

<ol>
    <li>Coffee</li>
    <li>Milk</li>
</ol>

## 定义列表

* 由\<dl>标签标识
* 列表项由\<dt>定义
* 列表项的定义由\<dd>定义

<dl>
    <dt>Coffee</dt>
    <dd>Black hot drink</dd>
    <dt>Milk</dt>
    <dd>White cold drink</dd>
</dl>



# HTML块

大多数HTML元素被定义为块级元素或者内联元素：

* 块级元素在浏览器显示时，通常以新行来开始和结束：如\<h1>,\<p>,\<ul>\<table>

* 内联元素在显示时通常不会以新行开始：\<b>,\<td>,\<a>,\<img>

我们也可以定义空的无意义的块级元素和内联元素

方便进行文档布局和设置文本样式

## \<div>

没有特定的含义，只表示块级元素

## \<span>

没有特定含义，只表示内联元素，可用作文本容器



# HTML内联框架

* \<iframe>用于在网页内显示网页
    * src属性指向隔离网页的位置
    * hight、wigth属性用于规定iframe的高度和宽度

# HTML头部元素

* \<head>元素是所有头部元素的容器。可以包含以下标签：

    * \<title>标签定义文档的标题

        * 定义浏览器工具栏中的标题
        * 提供页面被添加到收藏夹是显示的标题
        * 显示再搜索引擎结果中的标题

    * \<base>标签为页面上所有连接规定默认地址或默认目标

        ~~~html
        <head>
            <base href="index.html" />
            <base target="_blank" />
        </head>
        ~~~

    * \<link>标签定义文档与外部资源之间的关系

        ~~~html
        <head>
            <link rel="stylesheet" type="text/css" href="mystyle.css" />
        </head>
        ~~~

    * \<style>标签为HTML文档定义样式信息

        ~~~html
        <head>
            <style type="text/css">
                body {background-color:yellow}
                p (color:blue)
            </style>
        </head>
        ~~~

    * \<meta>标签提供关于HTML文档的元数据(metadata)

        元数据可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。

    * \<script>标签用于定义客户端脚本，比如Javascript

# HTML实体

| 显示结果 | 描述              | 实体名称           | 实体编号 |
| :------- | :---------------- | :----------------- | :------- |
|          | 空格              | \&nbsp;            | \&#160;  |
| <        | 小于号            | \&lt;              | \&#60;   |
| >        | 大于号            | \&gt;              | \&#62;   |
| &        | 和号              | \&amp;             | \&#38;   |
| "        | 引号              | \&quot;            | \&#34;   |
| '        | 撇号              | \&apos; (IE不支持) | \&#39;   |
| ￠       | 分（cent）        | \&cent;            | \#162;   |
| £        | 镑（pound）       | \&pound;           | \&#163;  |
| ¥        | 元（yen）         | \&yen;             | \#165;   |
| €        | 欧元（euro）      | \&euro;            | \&#8364; |
| §        | 小节              | \&sect;            | \&#167;  |
| ©        | 版权（copyright） | \&copy;            | \&#169;  |
| ®        | 注册商标          | \&reg;             | \&#174;  |
| ™        | 商标              | \&trade;           | \&#8482; |
| ×        | 乘号              | \&times;           | \&#215;  |
| ÷        | 除号              | \&divide;          | \&#247;  |

# HTML表单

## \<form>

用于定义HTML表单

有以下属性：

* action定义了提交表单时要执行的操作，通常值为指向脚本文件的路径，当提交后，表单将发送到该脚本处理
* target规定提交表单后再何处显示响应：
    * \_blank 显示在新窗口或选项卡中
    * _self （默认值）显示在当前窗口中
    * _parent 显示在父框架中
    * _top 显示在窗口的整个body中
    * framename 显示在命名的iframe中
* method指定提交表单数据时使用的HTTP方法：
    * get（默认）:适用于非安全的小量数据
        * 会将表单以键值对的形式追加到URL
        * URL长度受限（2048字符）
    * post：适用于包含敏感和个人信息的表单
        * 将表单数据附加到HTTP请求的正文中
        * 没有大小限制，可用于发送大量数据
* autocomplete规定表单是否打开自动完成功能：
    * on开启
    * off关闭

* novalidate规定在提交表单时不对表单数据进行验证（没有值）





## \<input>

定义了用于用户输入的表单内容

有以下属性：

* typt定义input输入的形态：
    * text:定义单行输入字段
    * password：定义密码字段
    * radio:定义单选按钮输入
    * submit:定义提交表单数据到表单处理程序的按钮
    * checkbox：定义复选框
    * button：定义按钮
    * number：用于包含数字的输入字段
    * date：包含日期的输入字段
    * color：包含颜色的输入字段
    * range：包含一定范围内的滑块控件输入字段
    * month：允许用户输入月份和年份
    * week：允许用户选择周和年
    * time：允许用户选择时间（无时区）
    * datetime：允许用户选择日期和时间(有时区)
    * datetime-local:允许用户选择日期和时间(无时区)
    * email：用于包含电子邮件地址的输入字段
    * search：用于搜索字段
    * tel：用于包含电话号码的输入字段
    * url：用于包含URL地址的输入字段

* name定义输入字段的名字，每个\<input>标签**必须**有名字
* value规定输入字段的初始值

* readonly规定输入字段为只读（不需要值）

* disabled规定输入字段时禁用的（不需要值）

    * 被禁用的元素时不可用不可点击的
    * 被禁用的元素不会被提交

* size规定输入字段的尺寸（可输入的字符长度）

* maxlength属性规定输入字段允许的最大长度

* autocomplete规定输入字段是否打开自动完成功能：

    autocomplete 属性适用于 \<form> 以及如下\<input> 类型：text、search、url、tel、email、password、datepickers、range 以及 color。

    * on开启
    * off关闭

    **提示：**您可以把表单的 autocomplete 设置为 on，同时把特定的输入字段设置为 off，反之亦然。

* autofocus如果设置，规定当页面加载时\<input>元素自动获得焦点

* form属性规定输入字段所属的一个或多个表单（多个表单用空格分隔
    ）

* height和width规定\<input>元素的高度和宽度

* min和max规定\<input>元素的最大值和最小值

    min 和 max 属性适用于如需输入类型：number、range、date、datetime、datetime-local、month、time 以及 week。

* pattern规定用于检查\<input>元素值的正则表达式

    pattern 属性适用于以下输入类型：text、search、url、tel、email、and password。

* placeholder规定用以描述输入字段预期值的提示

    placeholder 属性适用于以下输入类型：text、search、url、tel、email 以及 password。

* required如果设置，则规定在提交表单中之前必须填写该输入字段(无值)

    required 属性适用于以下输入类型：text、search、url、tel、email、password、date pickers、number、checkbox、radio、and file.

* step规定\<input>元素的合法数字间隔

    step 属性适用于以下输入类型：number、range、date、datetime、datetime-local、month、time 以及 week。



## \<label>

为 input 元素定义标注（标记）。

属性for：值为id，将label绑定到\<input>标签





## \<select>

定义下拉列表

* \<option>元素定义待选择的选项
    * value：表示待选项在表单中对应的值
    * selected：表示预选项



## \<textarea>

定义多行输入字段

有属性：

* rows定义行数
* cols定义文本域宽度



## \<button>

定义可点击的按钮
