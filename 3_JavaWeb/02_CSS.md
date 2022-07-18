# CSS简介

* CSS指层叠样式表(Cascading Style Sheets)或者级联样式表

* 用于定义网页的样式，设计和布局

* 语法：

    ~~~CSS
    选择器 {
        属性:值;
        属性:值;
        属性:值;
    }
    ~~~

# CSS选择器

## 简单选择器

| 名称       | 语法              | 作用                   |
| ---------- | ----------------- | ---------------------- |
| 元素选择器 | `element`         | 选取指定元素名称的元素 |
| id选择器   | `#id`             | 选取指定id的元素       |
| 类选择器   | `.class`          | 选取指定类的元素       |
| 通用选择器 | `*`               | 选取所有元素           |
| 分组选择器 | `element,element` | 选取多个指定元素       |

## 组合选择器

| 名称           | 语法    | 作用                           |
| -------------- | ------- | ------------------------------ |
| 后代选择器     | `space` | 匹配指定元素的所有后代元素     |
| 子选择器       | `>`     | 匹配指定元素的所有子元素       |
| 相邻兄弟选择器 | `+`     | 匹配指定元素后的相邻同级元素   |
| 通用兄弟选择器 | `~`     | 匹配指定元素后的所有的同级元素 |

## 伪类选择器

根据特定状态选取元素

| 选择器           | 作用                                      |
| ---------------- | ----------------------------------------- |
| `:link`          | 选取为被访问的链接                        |
| `:hover`         | 选取鼠标浮动在其上的元素~[1]~             |
| `:visited`       | 选取已被访问的链接                        |
| `:active`        | 选取活动元素（被鼠标点击时）              |
| `:checked`       | 选取已被选中的input元素(单选按钮和复选框) |
| `:empty`         | 选取没有子元素的元素                      |
| `:not(selector)` | 选取未被selector指定的元素                |
| `:valid`         | 选取有有效值的表单元素~[2]~               |
| `:invalid`       | 选取无效的表单元素                        |

**注1：**若:hover选取的是有:link和:visited样式的a标签，那么hover必须定义在:link和:visited之后,样式才生效

**注2：**:valid适用于有限制的表单元素，例如拥有min和max属性的input元素

## 伪元素选择器

用于设置元素指定部分的样式

| 选择器           | 作用                              |
| ---------------- | --------------------------------- |
| `::after`        | 在被选元素内容的后面插入内容~[1]~ |
| `::before`       | 在被选元素内容的前面插入内容~[1]~ |
| `::first-letter` | 选取被选元素的首字母~[2]~         |
| `::first-line`   | 选取被选元素的首行~[2]~           |
| `::selection`    | 选取被用户选中的内容              |

**注1：**通过content属性插入数据

**注2：**只适用于块级元素

## 属性选择器

| 选择器               | 作用                                  |
| -------------------- | ------------------------------------- |
| `[attribute]`        | 选取带有指定属性的元素                |
| `[attribute=value]`  | 选取带有指定元素和值的元素            |
| `[attribute~=value]` | 选取属性值包含指定**词**的元素~[1]~   |
| `[attribute|=value]` | 选取属性值以指定**词**开头的元素~[1]~ |
| `[attribute^=value]` | 选取属性值以指定值开头的元素          |
| `[attribute$=value]` | 选取属性值以指定值结尾的元素          |
| `[attribute*value]`  | 选取属性值包含指定值的元素            |

**注1：**值必须是完整或独立的单词



# 插入CSS样式表的方法

## 外部

在head部分的\<link>元素内包含对外部样式表的引用

## 内部

在\<style>元素中对样式表进行定义

## 内联

在元素内用过style属性定义样式

## 优先级

内联>内部>外部>浏览器默认





# 颜色

## 标准颜色名

CSS/HTML支持140多种标准颜色名，一下提供常用的颜色：

<table>
    <tr>
    	<th>颜色</th>
        <th>名称</th>
        <th>演示</th>
    </tr>
    <tr>
    	<td>red</td>
        <td>红</td>
        <td style="background-color:red;"></td>
    </tr>
    <tr>
    	<td>orange</td>
        <td>橙</td>
        <td style="background-color:orange;"></td>
    </tr>
    <tr>
    	<td>yellow</td>
        <td>黄</td>
        <td style="background-color:yellow;"></td>
    </tr>
    <tr>
    	<td>green</td>
        <td>绿</td>
        <td style="background-color:green;"></td>
    </tr>
    <tr>
    	<td>blue</td>
        <td>蓝</td>
        <td style="background-color:blue;"></td>
    </tr>
    <tr>
    	<td>indigo</td>
        <td>靛</td>
        <td style="background-color:indigo;"></td>
    </tr>
    <tr>
    	<td>violet</td>
        <td>紫</td>
        <td style="background-color:violet;"></td>
    </tr>
    <tr>
    	<td>black</td>
        <td>黑</td>
        <td style="background-color:black;"></td>
    </tr>
    <tr>
    	<td>white</td>
        <td>白</td>
        <td style="background-color:white;"></td>
    </tr>
    <tr>
    	<td>gray</td>
        <td>灰</td>
        <td style="background-color:gray;"></td>
    </tr>

## RGB颜色

* 在CSS中可以用下面公式指定RGB值：`rgb(red,green,blue)`

* 例如

<div style="background-color:rgb(255,0,0);">
    <p style="color:white" align="center">
        演示颜色rgb(255,0,0)
    </p>
</div>

## RGBA颜色

* 是具有alpha铜套的RGB颜色值的扩展，它指定了颜色的不透明度

* alpha的范围在0.0（完全透明）和1.0（完全不透明）之间

* 演示

<div>
    <p style="background-color:rgba(255,0,0,0.3);color:white;" align="center">a=0.3</p>
    <p style="background-color:rgba(255,0,0,0.6);color:white" align="center">a=0.6</p>
    <p style="background-color:rgba(255,0,0,1.0);color:white" align="center">a=1.0</p>

## HEX颜色

* 在CSS中可以用一下格式的十六进制值指定颜色

    `#rrggbb`

* 例如

<div style="background-color:#0000ff;">
    <p style="color:white" align="center">
        演示颜色#0000ff
    </p>
</div>

# 背景

## 背景颜色

`background-color`属性指定背景的颜色

## 背景图像

`background-image`属性指定背景的图像

属性值为`url("src_path")`

## 背景重复

默认情况下，`background-image`属性在水平和垂直方向上都重复图像

`background-repeat`属性指定指定背景图像的重复规则

属性值：

* repeat-x:仅在水平方法重复
* repeat-y:仅在垂直方法重复
* no-repeat：不重复

background-repeat属性值为no-repeat时，可以设置backgroud-position属性，

`background-position`属性指定背景图片的位置：

属性值：

* center
* left
* right
* top
* botton



## 背景附着

`background-attachment`属性指定背景图像是滚动的还是固定的（不会随页面的其他部分一起滚动）

属性值：

* fixed
* scroll(默认)

## 背景属性简写

* `background`属性是背景属性的简写属性，可以在一条属性中声明所有的背景属性

* 使用简写属性时，属性值的顺序为：

    color->image->repeat->attachment->position



# 边框

## 边框样式

`border-style`属性指定边框类型，只有指定了该属性，才能指定边框的其他属性

可以设置一到四个值（用于上边框、右边框、下边框和左边框）。

有属性值：

* dotted 点线边框
* dashed 虚线边框
* solid 实现边框
* double 双边框
* groove 3D坡口边框（凹槽）~[1]~
* ridge 3D脊线边框~[1]~
* inset 3Dinset边框~[1]~
* outset 3Doutset边框~[1]~

* none 无边框
* hidden 隐藏边框

**注1：**效果取决于border-color值

* 演示

<div align="center">
    <p style="border-style:dotted;">点状边框</p>
    <p style="border-style:dashed;">虚线边框</p>
    <p style="border-style:solid;">实现边框</p>
    <p style="border-style:double;">双线边框</p>
    <p style="border-style:groove;">凹槽边框</p>
    <p style="border-style:ridge;">垄状边框</p>
    <p style="border-style:inset;">3D inset边框</p>
    <p style="border-style:outset;">3D outset边框</p>
    <p style="border-style:none;">无边框</p>
    <p style="border-style:hiden;">隐藏边框</p>
    <p style="border-style:dotted dashed solid double;">混合边框</p>

## 边框宽度

`border-width`属性指定四个边框的宽度

可以设置一到四个值（用于上边框、右边框、下边框和左边框）。

属性值：

* 特定大小
* thin
* medium
* thick

演示：

<div align="center">
    <p style="border:solid thin">thin</p>
    <p style="border:solid medium">medium</p>
    <p style="border:solid thick">thick</p>
    <p style="border:solid 1cm">1cm</p>
    <p style="border-style:solid;border-width:thin medium thick 1cm ">混合长度</p>

## 边框颜色

`border-color`属性用于设置四个边框的颜色。

可以设置一到四个值（用于上边框、右边框、下边框和左边框）。

如果未设置 `border-color`，则它将继承元素的颜色。

## 边框各边

有一些属性可以用于指定每个边框

| style               | color               | width               |
| ------------------- | ------------------- | ------------------- |
| border-top-style    | border-top-color    | border-top-sidth    |
| border-right-style  | border-right-color  | border-right-sidth  |
| border-bottom-style | border-botton-color | border-botton-sidth |
| border-left-style   | border-left-color   | border-left-sidth   |

并且，style,color,width都可以指定4个值，以border-style为例

* 设置四个值：依次指定：上 右 下 左 边框的样式
* 设置三个值：依次指定：上 左右 下 边框的样式
* 设置两个值：依次指定：上下 左右 边框的样式
* 设置一个值：指定上下左右边框的样式

## 边框属性简写

`border`属性指定边框的简写属性：

border-top,border-botton,border-right,border-right是指定边框的简写属性







## 圆角边框

`border-radius`指定边框为圆角边框

属性值为大小单位，越大越圆

# 框模型

所有的HTML元素都可视为方框

对于每个HTML元素，都有：外边框，边框，内边框，以及实际的内容

![CSS边框模型](..\img\boxmodel.gif)

对不同的部分：

* 内容：框的内容，其中显示文本和图像
* 内边框：清除内容周围的区域，内边框是透明的
* 边框：围绕内边框和内容的边框
* 外边框：清除边界外的区域，外边框是透明的

**提示：**背景应用于由内容和内边距、边框组成的区域。



## 外边距

`margin`属性定义外边框大小,可定义1到4个属性值

不同数量的值的作用方式与边框一样

和边框一样，可以为每一侧外边框单独定义样式：

margin-top,margin-right,margin-botton,margin-left

属性值：

* auto：浏览器来计算外边框
* length（单位：px,pt,cm等）
* inherit：指定从父元素继承外边框
* %：指定以包含元素宽度的百分比计的外边框

**注意：**外边框会自动合并



## 内边距

`padding`属性定义内边框大小,可定义1到4个属性值

不同数量的值的作用方式与边框一样

和边框一样，可以为每一侧内边框单独定义样式：

padding-top,padding-right,padding-botton,padding-left

属性值：

* length（单位：px,pt,cm等）
* inherit：指定从父元素继承外边框
* %：指定以包含元素宽度的百分比计的外边框

## 高度和宽度

`height`,`width`设置元素内容的高度和宽度

有属性值:

* auto 浏览器计算值
* length 长度单位
* % 百分比定义值
* initial 默认值
* inherit 从其父值继承高度/宽度

<hr>
`max-width` 设置元素的最大宽度

有属性值

* length
* %
* none（默认，即没有最大宽度）

该值可以让元素适应浏览器窗口，当窗口宽度小于max-width的值后随着窗口宽度变小，元素宽度也会随着变小



# 轮廓

**注意：**轮廓与边框不同！不同之处在于：轮廓是在元素边框之外绘制的，并且可能与其他内容重叠。同样，轮廓也不是元素尺寸的一部分；元素的总宽度和高度不受轮廓线宽度的影响。

## 轮廓样式

`outline-style` 属性定义轮廓样式，有属性值：

有属性值：

* dotted 点线轮廓
* dashed 虚线轮廓
* solid 实现轮廓
* double 双轮廓
* groove 3D坡口轮廓
* ridge 3D脊线轮廓
* inset 3Dinset轮廓
* outset 3Doutset轮廓

* none 无轮廓
* hidden 隐藏轮廓

**注意：**与边框一样，只有定义了style样式，其他的轮廓属性才会生效

## 轮廓宽度

`outline-width`属性指定轮廓宽度：

属性值：

* 特定大小
* thin
* medium
* thick

## 轮廓颜色

`outline-color`属性指定轮廓颜色

除了CSS指定的颜色值，该属性还可以指定值：

invert 执行颜色反转（确保轮廓可见）

## 轮廓简写

与边框属性一样，`outline`属性用于简写轮廓属性

`outline`可以在

* `outline-width`

* `outline-style`

* `outline-color`

中指定1个或多个值，没有顺序限制

## 轮廓偏移

`outline-offset` 属性在元素的轮廓与边框之间添加空间。元素及其轮廓之间的空间是透明的。

属性值为长度单位



# 文本

## 文本颜色

`color`指定文本颜色

属性值：

* 颜色名
* RGB值
* HEX值

## 文本对齐

`text-align`属性指定文本的水平对齐方式

属性值：

* center
* left
* right
* justify:使文本每一行具有相等的宽度，且左右边距是直的
* inherit：从父元素继承

<hr>

`vertical-align`属性指定元素的垂直对齐方式

属性值：

| 值          | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| baseline    | 默认。元素放置在父元素的基线上。                             |
| sub         | 垂直对齐文本的下标。                                         |
| super       | 垂直对齐文本的上标                                           |
| top         | 把元素的顶端与行中最高元素的顶端对齐                         |
| text-top    | 把元素的顶端与父元素字体的顶端对齐                           |
| middle      | 把此元素放置在父元素的中部。                                 |
| bottom      | 把元素的顶端与行中最低的元素的顶端对齐。                     |
| text-bottom | 把元素的底端与父元素字体的底端对齐。                         |
| length      |                                                              |
| %           | 使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。 |
| inherit     | 规定应该从父元素继承 vertical-align 属性的值。               |

## 文本装饰

`text-decoration`属性指定文本装饰

属性值：

* none：无文本装饰（常用于删除链接文本的下划线）
* overline：上划线
* line-through：删除线
* underline：下划线
* blink：闪烁文本
* inherit：从父元素继承

## 文本转换

`text-transform`属性指定文本中的大小写字母

属性值：

* uppercase：全部转换成大写
* lowercase：全部转换成小写
* capitallize：首字母大写，其他小写
* none：默认
* inherit：从父元素继承

## 文本间距

`text-indent`指定首行缩进

属性值：

* length

<hr>

`letter-spacing`指定字符间距

属性值：

* length

<hr>

`line-height`指定行高

属性值：

* %：大多数浏览器的默认值为1.2或1.1

<hr>

`word-sapcing`指定单词间距

属性值：

* length

<hr>

`white-sapce`指定元素内部空白的处理方式

属性值：

* nowrap：禁用文本换行

## 文本阴影

`text-shadow`为文本添加阴影

可指定2到4个属性值，含义依次是：

水平阴影（必选），垂直阴影（必选），模糊效果，颜色，



# 字体

`font-family` 属性规定文本的字体。

font-family 属性应包含多个字体名称作为“后备”系统，以确保浏览器/操作系统之间的最大兼容性。请以您需要的字体开始，并以通用系列结束（如果没有其他可用字体，则让浏览器选择通用系列中的相似字体）。字体名称应以逗号分隔。

**注释：**如果字体名称不止一个单词，则必须用引号引起来，例如："Times New Roman"。

## 字体样式

`font-style`指定字体斜体

属性值：

* normal：正常显示
* italic：斜体显示
* oblique：文本倾斜（与斜体相似，支持较少）

<hr>

`font-weight`指定字体粗细

属性值：

* normal
* lighter
* bold
* number（属于${ \{x|x=100\times y,y 属于0到9\} }$

<hr>

`font-variant`指定字体是否以small-caps字体(小型大写字母)显示文本

在 small-caps 字体中，所有小写字母都将转换为大写字母。但是，转换后的大写字母的字体大小小于文本中原始大写字母的字体大小。

属性值：

* normal：正常显示文本
* small-caps：以small-caps字体显示文本

## 字体大小

`font-size`属性设置文本大小

属性值：

* 像素值（px）
* 相对字体大写(em)(1em等于当前字体大小)
* 响应式字体大小(vm)(1vm=视口宽度的1%)

## 字体属性简写

`font`指定字体属性的简写

是以下属性的简写：

- `font-style`
- `font-variant`
- `font-weight`
- `font-size/line-height`
- `font-family`

**注意：**`font-size` 和 `font-family` 的值是必需的。如果缺少其他值之一，则会使用其默认值。
