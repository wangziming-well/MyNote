# jQuery简介

jQuery 是一个 JavaScript 函数库。它对JS对dom对象的操作进行了封装

jQuery 库包含以下特性：

- HTML 元素选取
- HTML 元素操作
- CSS 操作
- HTML 事件函数
- JavaScript 特效和动画
- HTML DOM 遍历和修改
- AJAX
- Utilities

在jQuery中：

`$`是jQuery的别称，

jQuery就是jQuery库提供的一个函数

也是JQuery提供的一个类

# JQuery核心函数

jQuery()是jQuery的核心函数，根据参数的不同，能提供不同的功能

## jQuery(selector[,context])

通过指定的CSS选择器匹配并返回指定的HTML元素对应的jQuery对象

* `selector`:用来查找的CSS字符串

* `context`待查找的DOM元素集，文档或者jQuery对象

    如果未指定，则默认查找document

## 封装

* `jQuery(element|elementArray)`

    将DOM的element对象或数组对象封装jQuery对象

* ` jQuery(object)`

    将JS对象封装成jQuery对象

* `jQuery(jQueryObject)`

    复制jQuery对象 

* `jQuery()`

    返回一个空的jQuery对象



## jQuery(callback)

`$(document).ready()`的简写

当DOM文档载入完成后执行指定的函数

* `callback`:回调函数

------

通过以上函数返回的jQuery对象，可以实现对HTML元素的各个方面的操作：

属性、CSS、文档处理、事件、效果



# jQuery对象访问

* `each(callback)`

    以每一个匹配的元素作为上下文来执行指定函数，也就是说，每次执行传递进来的函数时，函数中的`this`关键字的指向时不同的DOM元素

    callback有一个参数i，从0开始，每次迭代加一

* `size()`   和`length`

    返回jQuery对象中元素的个数

* `get([index])`

    返回指定元素的dom对象

    如果没有参数，默认返回匹配的DOM元素集合



# 属性

* `attr(name|properties|key,valeu|fn)`

    设置或者返回被选元素的属性

    获取属性是获取第一个元素的属性

    设置属性是设置所有匹配的属性

    * `name`属性名称
    * `properties`键值对对象

    * `key,value`设置对应属性的值
    * `key,function(index,attr)`通过函数设置属性值，为函数的返回值



* `removeAttr(name)`

    从每一个匹配的元素删除指定属性

* `addClass(class|fn)`

    为每个匹配的元素添加指定的类名

    * `class`一个或多个要添加到元素中的CSS类名，请用空格分开
    * `function(index, class)`此函数必须返回一个或多个空格分隔的class名。接受两个参数，index参数为对象在这个集合中的索引值，class参数为这个对象原先的class属性值。

* `removeClass([class|fn])`

    从所有匹配的元素中删除全部或者指定的类

    * `class`一个或多个要删除的CSS类名，请用空格分开
    * `function(index,class)`此函数必须返回一个或多个空格分隔的class名。接受两个参数，index参数为对象在这个集合中的索引值，class参数为这个对象原先的class属性值。

* `html([val|fn])`

    取得第一个匹配元素的html内容

    或设置所有匹配元素的html内容

    * `val`用于设定HTML内容的值
    * `function(index,html)`此函数返回一个HTML字符串。接受两个参数，index为元素在集合中的索引位置，html为原先的HTML值

* `text([val|fn])`

    获取所有匹配元素的内容，多个元素会将文本顺序拼接返回

    设置所有匹配元素的内容

* `css(name|pro|[,val|fn])`

    访问匹配元素的样式属性。

    * `name`属性名称
    * `properties`键值对对象

    * `name,value`设置对应属性的值
    * `name,function(index,value)`通过函数设置属性值，为函数的返回值



# 文档处理

* `append(content|fn)`向每个匹配的元素内部追加内容
* `prepend(content|fn)`向每个匹配的元素内部前置内容

* `after(content|fn) `在每个匹配的元素之后插入内容

* `before(content|fn) `在每个匹配的元素之前插入内容

* `empty()`删除匹配的元素集合中所有的子节点



`content`:要追加的内容 可以是String Element ，jQuery

`function(index, html)`:返回一个HTML字符串，用于追加到每一个匹配元素的里边。接受两个参数，index参数为对象在这个集合中的索引值，html参数为这个对象原先的html值。

# 事件

* `read(fn)`当DOM载入就绪可以查询及操纵时绑定一个要执行的函数。

jQuery封装了常用的事件，可以直接通过jQuery对象调用，以click为例：

* `click([[data],fn])`触发每一个匹配元素的click事件
    * `data`:可传入data供函数fn处理。
    * `fn`:在每一个匹配元素的click事件中绑定的处理函数。



# 效果

* `show([speed[,easing][,fn]])`显示隐藏的匹配元素。
    * `speed`三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)v
    * `easing`:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"
    * `fn`在动画完成时执行的函数，每个元素执行一次

* `hide([speed,[easing],[fn]])`隐藏显示的元素

