# JSP

Java Server Page java服务页面技术

Jsp= HTML +java代码

jsp本质是servlet 被服务器创建并运行

运行流程：

客户端发起请求->服务器将.jsp文件转译为.java文件->jvm将.java文件编译为.class文件->运行时将.class文件转变为.html静态网页



## JSP脚本

Jsp脚本就是Java代码片段，有以下三种：

* `<%..%>`：放置java片段。在一个页面中所有片段相通
* `<%=...%>`:放置java表达式，用于页面输出（相当于response.getWriter().write().
* `<%!...%>`：定义Java类，只能在本页面定义，几乎不用

## JSP指令

JSP指令告诉JSP引擎处理JSP页面的非输出部分

基本语法

~~~jsp
<%@ 指令名 属性名="值" %>
~~~

### page指令

用于定义JSP页面的各种属性，最好放在JSP页面的起始位置

JSP2.0规范定义的page指令完整语法：

~~~jsp
<%@ page 
	[ language="java" ] 
	[ extends="package.class" ] 
	[ import="{package.class | package.*}, ..." ] 
	[ session="true | false" ] 
	[ buffer="none | 8kb | sizekb" ] 
	[ autoFlush="true | false" ] 
	[ isThreadSafe="true | false" ] 
	[ info="text" ] 
	[ errorPage="relative_url" ] 
	[ isErrorPage="true | false" ] 
	[contentType="mimeType [ ;charset=characterSet ]" | "text/html ; charset=ISO-8859-1" ]
	[ pageEncoding="characterSet | ISO-8859-1" ] 
	[ isELIgnored="true | false" ] 
%>
~~~

~~~
[1]import属性：指定 JSP 页面转换成 Servlet时应该导入的包。

[2]pageEncoding属性：设置JSP页面翻译成Servlet源文件时使用的字符集。

[3]contentType属性：设置 Content-Type 响应报头，标明即将发送到客户程序的文档的 MIME 类型以及浏览器对响应内容的解码字符集。 

[4]errorPage属性：指定当前JSP抛出异常时的转发页面。

[5]isErrorPage属性：指定当前页面是不是一个显示错误消息的页面，如果是，则会自动创建exception对象，否则就不会创建exception对象。

[6]session属性：控制页面是否参与HTTP会话，其本质是要不要自动创建session隐含对象以供使用。

[7]isELIgnored属性：指定当前页面是否忽略EL表达式，如果忽略，EL表达式的内容将会原封不动的输出到浏览器端。
~~~

### include指令

用于让当前页面与指定页面合并，一般不用

语法：

~~~jsp
<%@ include file="relativeURL"%>
~~~

### taglib指令

用于引入标签库并设置标签库的前缀

语法：

~~~jsp
<%@ taglib prefix="标签前缀(别名)" uri="标签库URI"
~~~



## JSP内置对象

JSP对servlet进行了一定的封装，服务器提供了9个隐式对象，可以直接使用

| 对象名          | 类型                                   |
| --------------- | -------------------------------------- |
| request         | javax.servlet.http.HttpServletRequest  |
| response        | javax.servlet.http.HttpServletResponse |
| session         | javax.servlet.http.HttpSession         |
| application     | javax.servlet.ServletContext           |
| config          | javax.servlet.ServletConfig            |
| exception       | java.lang.Throwable                    |
| out             | javax.servlet.jsp.JspWriter            |
| **pageContext** | javax.servlet.jsp.PageContext          |
| page            | java.lang.Object当前对象this           |

## JSP域对象

| 域对象      | 作用范围    | 起始时间    | 结束时间    |
| ----------- | ----------- | ----------- | ----------- |
| pageContext | 当前JSP页面 | 页面加载    | 离开页面    |
| request     | 同一个请求  | 收到请求    | 响应        |
| session     | 同一个会话  | 开始会话    | 结束会话    |
| application | 当前Web应用 | Web应用加载 | Web应用卸载 |

域对象是我们传递参数的容器

域对象是基于MAP格式的容器，数据以键值对的形式储存：

* `void setAttribute(String key,Object value)`:保存数据
* `Object getAttribute(String key)`:获取数据
* `void removeAttribute(String name)`:删除数据

# JSP2.0

JSP2.0规范JSP为纯标签语言，即不包含<%%><%=%>等

将java脚本替换为标签，非Java人员也可以使用

为此引入了EL表达式(替代<%=%>)与JSTL技术(替代<%%>)



## EL表达式

EL(Expression Language)表达式语言，对应`<%=...%>`

格式：`${...}`

在el表达式中可以进行算术运算，逻辑运算（只有短路），比较运算，符号与Java基本一致，

但`+`在el表达式中只进行加法运算，没有拼接功能

除此之外还有运算符 `empty`：

可以判断字符串、数据、集合的长度是否为0，为0返回true

### EL表达式获取值

* 获取域对象的值：`${keyname}` 等价于`getAttribute()`

    依次从小域到大域检索键名，即检测次序：

    pageContext->request->session->application

* 获取指定域的值：
    * pageScope：${pageScope.name}等同与pageContext.getAttribute(“name”)；
    * requestScope：${requestScope.name}等同与request.getAttribute(“name”)；
    * sessionScoep： ${sessionScope.name}等同与session.getAttribute(“name”)；
    * applicationScope：${applicationScope.name}等同与application.getAttribute(“name”)；

* 获取java对象的属性（不论public或private，应该用的反射）：

    `${person.name}`相当于：`person.getName()`

* 获取List和数组的值：`${array[i]}`,`${list[i]}`

* 获取map的值：`${map.key}`，`${map["key"]}`

### EL表达式的内置对象

| pageScope        | page域        |
| ---------------- | ------------- |
| requestScope     | request域     |
| sessionScope     | session域     |
| applicationScope | appliaction域 |
| param；          |               |
| paramValues；    |               |
| header；         |               |
| headerValues；   |               |
| initParam；      |               |
| cookie；         | 会话管理对象  |
| pageContext；    | 上下文        |





## JSTL标签库

Java Server Pages Standard Tag Library——JSP标准标签库。

应用于：基本输入输出，流程控制等

JSTL提供了5大类标签函数库，我们只学核心标签库



### 前置工作

* 导入jar包：jstl.jar    standard.jar

* 引入标签库：

    ~~~jsp
    <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
    ~~~

### 常用标签

* out 输出指定值
    * value 指定输出的值
    * default value表达式为null时，输出的默认值

* set  设置变量值和对象属性
    * value 要储存的值
    * target 要修改的属性所属的对象，(值必须是对象的引用)
    * property 要修改的属性
    * var 存储属性的变量
    * scope var属性的作用域

* remove 删除域中的指定值
    * var 要移除的键值
    * scope var所属的作用域(默认为所有作用域)

* if 条件判断
    * test 判断的条件，值只能是true或false
    * var 储存test的结果
    * scope var属性的作用域
* choose多重条件判断  子标签：
    * when 只有一个属性test
    * otherwise
* forEach遍历：
    * 普通for循环
        * var 当前循环的变量名
        * begin 循环开始的元素
        * end 循环结束的元素
        * step 每一次迭代的步长
    * 增强for循环
        * items 循环体，可以是数组，集合等可迭代对象
    * varStatus 代表循环状态(对象)的变量名称
