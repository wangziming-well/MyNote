# DOM简介

DOM ：Document Object Model

当页面被加载时，浏览器会创建DOM

JS通过访问DOM对象，能动态的创建、改变HTML元素

## 什么是 DOM

DOM 是一项 W3C (World Wide Web Consortium) 标准。

DOM 定义了访问文档的标准：

> “W3C 文档对象模型（DOM）是中立于平台和语言的接口，它允许程序和脚本动态地访问、更新文档的内容、结构和样式。”

W3C DOM 标准被分为 3 个不同的部分：

- Core DOM - 所有文档类型的标准模型
- XML DOM - XML 文档的标准模型
- HTML DOM - HTML 文档的标准模型

## 什么是 HTML DOM？

HTML DOM 是 HTML 的标准*对象*模型和*编程接口*。它定义了：

- 作为*对象*的 HTML 元素
- 所有 HTML 元素的*属性*
- 访问所有 HTML 元素的*方法*
- 所有 HTML 元素的*事件*

JS通过访问document对象访问和操作 HTML 的实例。







# DOM对象

Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。

**提示：**Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

## 属性

* `body` 访问body元素
* `cookie`返回或设置当前文档有关的所有cookie
* `domain`返回当前文档的域名
* `lastModified`返回文档的最后修改日期和时间
* `referrer`返回载入当前文档的超链接的文档的URL
* `title`返回文档标题
* `URL`返回文档URL



## 方法

* `getElementById()`返回对拥有指定 id 的第一个对象的引用。
* `getElementsByName()`返回带有指定name的对象集合。
* `getElementsByTagName()`返回带有指定标签名的对象集合。

* `getElementsByClassName()` 返回带有指定class的对象集合
* `querySelectorAll() `查找指定CSS选择器的所有HTML元素对象的引用

这些方法返回HTML元素的对应对象的引用也就是Element对象



# Element对象

在 HTML DOM 中，Element 对象表示 HTML 元素。

dom提供了属性方法以获取，改变HTML元素的内容

下面提供一些常用的属性方法

## 属性

* `id`
* `innerHTML`

## 方法

* `setAttribute(attributename,attributevalue)`

* `removeAttribute(attributename)`



# Event

事件能够支持页面实现当用户进行某些操作时，触发对应的JS函数



## 向HTML元素分配事件

以click事件为例：

* 通过元素的事件属性

    ~~~html
    <button onclick="demo()">试一试</button>
    ~~~

* 通过element对象：

    ~~~js
    document.getElementById("btn").onclick = method
    ~~~

    

## 常用事件

* `click`：当用户点击指定元素时，发生此事件
* `focus`：当指定元素得焦时，发生此事件
* `blur`：当指定元素失焦时，发生此事件
* `input`：当\<input> 或 \<textarea> 元素的值发生改变时，会发生此事件。
* `submit`：当表单提交时，发生此事件

* `load`在对象已加载时，发生此事件。

# HTMLCollection

是HTML元素的类似数组的列表

由诸如`getElementsByTagName()`之类的方法会返回HTMLCollection



## 属性/方法

* `length `返回HTMLCollection中的元素数
* `item(index)`获取指定索引的HTML元素对象
* `namedItem(name)`获取指定ID或名称 的HTML元素对象 
