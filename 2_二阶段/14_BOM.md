# BOM

允许JS与浏览器窗口对话

加载到页面时浏览器会生成window对象，供JS使用

所有全局JS对象，函数，变量自动成为window对象的成员

全局变量时window对象的属性

全局函数是window对象的方法

document也是window对象的属性

调用当前窗口的方法和属性时，`window.`可以省略

`window.document <=> document`

# 属性

* `closed`返回窗口是否被关闭
* `name`设置或返回窗口的名称

* `opener`返回对创建该窗口的窗口的引用
* `parent`返回父窗口
* `frames[]`返回窗口中所有命名的框架。
* `document`对Document对象的只读引用
* `history`对History对象的只读引用
* `location`用于窗口或框架的 Location 对象
* `Navigator`对 Navigator 对象的只读引用
* `Screen`对 Screen 对象的只读引用

# 方法

## open()

`open([URL[,name[,features[,replace]]]])`打开一个新的浏览器窗口或查找一个已命名的窗口，并返回该窗口的window对象的引用

* URL：字符串，声明了要在新窗口中显示的文档的 URL。默认为空字符串

* name：字符串，声明了新窗口的名称

    如果该参数指定了一个已经存在的窗口，那么 open() 方法就不再创建一个新窗口，而只是返回对指定窗口的引用。此时features 将被忽略。

* features：字符串，声明了新窗口要显示的标准浏览器的特征

    字符串中的窗口特征用`,`隔开下面列举了窗口特征：

    | 窗口特征                  | 描述                                                         |
    | ------------------------- | ------------------------------------------------------------ |
    | channelmode=yes\|no\|1\|0 | 是否使用剧院模式显示窗口。默认为 no。                        |
    | directories=yes\|no\|1\|0 | 是否添加目录按钮。默认为 yes。                               |
    | fullscreen=yes\|no\|1\|0  | 是否使用全屏模式显示浏览器。默认是 no。处于全屏模式的窗口必须同时处于剧院模式。 |
    | height=pixels             | 窗口文档显示区的高度。以像素计。                             |
    | left=pixels               | 窗口的 x 坐标。以像素计。                                    |
    | location=yes\|no\|1\|0    | 是否显示地址字段。默认是 yes。                               |
    | menubar=yes\|no\|1\|0     | 是否显示菜单栏。默认是 yes。                                 |
    | resizable=yes\|no\|1\|0   | 窗口是否可调节尺寸。默认是 yes。                             |
    | scrollbars=yes\|no\|1\|0  | 是否显示滚动条。默认是 yes。                                 |
    | status=yes\|no\|1\|0      | 是否添加状态栏。默认是 yes。                                 |
    | titlebar=yes\|no\|1\|0    | 是否显示标题栏。默认是 yes。                                 |
    | toolbar=yes\|no\|1\|0     | 是否显示浏览器的工具栏。默认是 yes。                         |
    | top=pixels                | 窗口的 y 坐标。                                              |
    | width=pixels              | 窗口的文档显示区的宽度。以像素计。                           |

* `replace`：布尔值，规定了载到窗口的 URL 是在窗口的浏览历史中创建一个新条目，还是替换浏览历史中的当前条目。

## 对话框

* `alert(message)`

    显示带有一条指定消息和一个 OK 按钮的警告框。

* `confirm(message)`

    显示一个带有指定消息和 OK 及取消按钮的对话框。

    如果用户点击确定按钮，则 confirm() 返回 true。如果点击取消按钮，则 confirm() 返回 false。

    是一个就绪方法，调用 confirm() 时，将暂停对 JavaScript 代码的执行，在用户作出响应之前，不会执行下一条语句。

    在用户点击确定按钮或取消按钮把对话框关闭之前，它将阻止用户对浏览器的所有输入

* `prompt(text,defaultText)`

    显示可提示用户进行输入的对话框

    text：提示信息

    defaultText：输入框默认文本

    如果用户单击提示框的取消按钮，则返回 null。如果用户单击确认按钮，则返回输入字段当前显示的文本。

    在用户点击确定按钮或取消按钮把对话框关闭之前，它将阻止用户对浏览器的所有输入。在调用 prompt() 时，将暂停对 JavaScript 代码的执行，在用户作出响应之前，不会执行下一条语句。

## close()

`close()`

用于关闭浏览器方法

只有通过 JavaScript 代码打开的窗口才能够由 JavaScript 代码关闭。这阻止了恶意的脚本终止用户的浏览器。

# History

History对象包含用户在浏览器窗口中访问过的URL

## 属性

* `length`返回浏览器历史列表中的URL数量

## 方法

* `back()`加载history列表中当前一个URL
* `forward()`加载history列表中的下一个URL
* `go(number|URL)`加载history列表中某个具体页面
    * URL：history中的url
    * number：要访问的 URL 在 History 的 URL 列表中的相对位置。

# Location对象

Location对象包含相关当前URL的信息

## 属性

* `hash`	设置或返回从井号 (#) 开始的 URL（锚）。
* `host`	设置或返回主机名和当前 URL 的端口号。
* `hostname`	设置或返回当前 URL 的主机名。
* `href`	设置或返回完整的 URL。
* `pathname`	设置或返回当前 URL 的路径部分。
* `port`	设置或返回当前 URL 的端口号。
* `protocol`	设置或返回当前 URL 的协议。
* `search`	设置或返回从问号 (?) 开始的 URL（查询部分）

## 方法

* `assign(URL)`	加载新的文档。

* `reload()`	重新加载当前文档。

* `replace()`	用新的文档替换当前文档。

    replace不会在 History 对象中生成一个新的记录。当使用该方法时，新的 URL 将覆盖 History 对象中的当前记录。

# Navigator

Navigator 对象包含的属性描述了正在使用的浏览器。可以使用这些属性进行平台专用的配置。

虽然这个对象的名称显而易见的是 Netscape 的 Navigator 浏览器，但其他实现了 JavaScript 的浏览器也支持这个对象。

Navigator 对象的实例是唯一的，可以用 Window 对象的 navigator 属性来引用它

## 属性

* `appCodeName	`返回浏览器的代码名。
* `appMinorVersion	`返回浏览器的次级版本。
* `appName	`返回浏览器的名称。
* `appVersion	`返回浏览器的平台和版本信息。
* `browserLanguage	`返回当前浏览器的语言。
* `cookieEnabled	`返回指明浏览器中是否启用 cookie 的布尔值。
* `cpuClass	`返回浏览器系统的 CPU 等级。
* `onLine	`返回指明系统是否处于脱机模式的布尔值。
* `platform	`返回运行浏览器的操作系统平台。
* `systemLanguage	`返回 OS 使用的默认语言。
* `userAgent	`返回由客户机发送服务器的 user-agent 头部的值。
* `userLanguage`	返回 OS 的自然语言设置。

## 方法

* `javaEnabled()`	规定浏览器是否启用 Java。
* `taintEnabled()`	规定浏览器是否启用数据污点 (data tainting)。

# Screen

Screen 对象包含有关客户端显示屏幕的信息。

## 属性

* `availHeight	`返回显示屏幕的高度 (除 Windows 任务栏之外)。
* `availWidth	`返回显示屏幕的宽度 (除 Windows 任务栏之外)。
* `bufferDepth	`设置或返回调色板的比特深度。
* `colorDepth	`返回目标设备或缓冲器上的调色板的比特深度。
* `deviceXDPI	`返回显示屏幕的每英寸水平点数。
* `deviceYDPI	`返回显示屏幕的每英寸垂直点数。
* `fontSmoothingEnabled	`返回用户是否在显示控制面板中启用了字体平滑。
* `height	`返回显示屏幕的高度。
* `logicalXDPI	`返回显示屏幕每英寸的水平方向的常规点数。
* `logicalYDPI	`返回显示屏幕每英寸的垂直方向的常规点数。
* `pixelDepth	`返回显示屏幕的颜色分辨率（比特每像素）。
* `updateInterval	`设置或返回屏幕的刷新率。
* `width	`返回显示器屏幕的宽度。

# Console

Console 对象提供对浏览器调试控制台的访问。

## 方法

* log()	将消息输出到控制台。

* warn()	将警告消息输出到控制台。

* time()	启动计时器（可跟踪操作需要多长时间）。
* timeEnd()	停止以前由 console.time() 启动的计时器。