# Servlet接口

Servlet是Javaweb三大组件之一

是所有Servlet的顶级接口

servlet是多线程单例对象，；懒汉式，唯一对象在被第一次访问时由服务器创建对象，之后再对该servlet访问不会创建新对象

## 方法

* `public void init(ServletConfig config)`

    servlet被创建时调用该对象进行初始化

    ServletConfig对象由Servlet引擎负责创建，该域对象存储了web.xml文件中`<init-param>`配置的多个键值对，并提供了一个获取ServletContext对象的方法

* `public void service(ServletRequest req,ServletResponse resp)`

    客户端每对该servlet发送一次请求，就调用一次该方法

    ServletRequest对象和ServletResponse对象由Servlet创建，并传入

* `public void destroy()`

    服务器停止时，会释放Servlet，调用该方法

    一般不需要人为调用

* `public ServletConfig getServletConfig()`

    获取初始化参数

* `public String getServletInfo()`

    获取servlet信息

# GenericServlet 抽象类

对Servlet接口中的部分方法(init和destroy)添加了实现

# HttpServlet 抽象类

GenericServlet的子类，实现了http请求的处理，

http请求方式有delete，get,options,psot,put,tract等;该类提供了分别处理这些请求的方法

主要通过实现该类来创建servlet处理http请求

## 常用方法

* `protected void service(HttpServletRequest req,HttpServletResponse resp)`

    该方法默认判断请求类型，然后调用对应的执行方法

    所以如果重写方法，那么所有类型的请求都只能在该方法中处理

* `protected void doGet(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起get请求时，service默认调用该方法进行处理

* `protected void doPost(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起post请求时，service默认调用该方法进行处理

* `protected void doDelete(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起delete请求时，service默认调用该方法进行处理

* `protected void doHead(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起head请求时，service默认调用该方法进行处理

    该方法一般不需要被子类重写

* `protected void doOptions(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起options请求时，service默认调用该方法进行处理

    该方法一般不需要被子类重写

* `protected void doPut(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起put请求时，service默认调用该方法进行处理

* `protected void doTrace(HttpServletRequest req,HttpServletResponse resp)`

    当对该servlet发起trace请求时，service默认调用该方法进行处理

* `protected long getLastModified(HttpServletRequest req)`

    返回请求的最后修改时间，默认返回-1，

    HttpServlet接收到GET请求后，默认的service方法会先调用该方法，根据该方法的返回值：

    1. 负数：service会调用doGet方法生成响应信息返回给客户端
    2. 正数，且大于If-Modified-Since字段 或者If-Modified-Since字段不存在：service会调用doGet方法生成响应信息返回给客户端
    3. 正数，但小于If-Modified-Since字段：service会返回304状态给客户端，让客户端继续使用以前缓存的网页，不会再调用doGet方法

# HttpServletRequest

是ServletRequest的子接口

是域对象

封装了请求头与请求正文和请求行信息

提供请求转发与请求包含功能

## 获取请求行信息

* `String getMethod()`

    获取HTTP请求方式

* `String getRequestURL()`

    获取请求URL路径，即参数之前的所有信息

* `String getScheme()`

    获取请求协议

* `String getContextPath()`

    获取Servlet上下文路径(项目名)

* `String getRequestURI()`

    获取请求资源路径

* `String getQueryString()`

    获取请求参数

* `String getServletPath()`

    获取当前Servlet的映射路径

* `String getRemoteAddr()`

    获取客户端的IP地址

* `String getRemoteHost()`

    获取客户端主机名

* `String getServerName()`

    返回服务端主机名

* `String getServerPort()`

    返回服务器端口号

![](..\img\URL.png)

## 获取请求头信息

* `String getHeader(String name)`

    获取指定名称的请求头

* `Enumeration getHeaderNames()`

    获取所有请求头名称

* `int getIntHeader(String name)`

    获取值为int的请求头

* `String getContentType()`

    获取请求头Content-Type字段的值

* `Cookie[] getCookies()`

    获取请求头的cookies信息

* `int getContentLength()`

    获取请求头Content-Length字段的值

* `String getCharacterEncoding() `

    返回请求消息的字符集编码
    
* `void setCharacterEncoding()`

    设置请求消息的字符集编码

## 获取请求体信息

* `String getParameter(String name)`

    获取指定键的值

* `String[] getParameterValues(String name)`

    获取指定键的所有值

* `Enumeration getParameterNames()`

    以枚举获取所有键名

* `Map getParameterMap()`

    以Map获取表单所有键值对

## 请求转发

* `RequestDispatcher getRequestDispatcher(String path)`

    获取指定资源的转发对象

## 获取其他域对象

* `HttpSession getSession()`

    获取关联的会话对象，如果没有则创建新的seesion对象

* `ServletContext getServletContext()`

    获取上下文对象

# HttpServletResponse

通过response可以对客户端进行响应

可以设置响应行，响应头，响应体，并提供重定向功能

## 设置响应行

* `void setStatus(int status)`
* `void sendError(int sc)`

## 设置响应头

* `void addHeader(String name,String value)`

    增加响应头字段

* `void setHeader(String name,String value)`

    设置响应头字段

* `void addIntHeader(String name,int value)`

    增加值为int的响应头字段

* `void setIntHeader(String name,int value)`

    设置值为int的响应头字段

* `void addCookie(Cookie cookie)`

    添加cookies

* `void setContentType(String type)`

    设置Servlet输出内容的MIME类型已经编码格式，一般`type="text/html;charset=UTF-8"`

* `void setCharacterEncoding(String charset)`

    设置输出内容的编码格式

## 设置响应正文

* `ServletOutputStream getOutputStream()`

    获取正文的字节流输出对象

* `PrintWriter getWriter()`

    获取正文的字符流输出对象

## 重定向

* `void sendRedirect(String location)`

    向浏览器发送状态码为302的响应结果，让浏览器访问指定的URL

# Cookie

是服务器保存在浏览器上的信息文件

## 构造方法

* `public Cookie(String name,String value)`

## 发送和获取cookie

* 通过HttpServletRequest的getCookies()方法获取

* 通过HttpServletResponse的addCookie()方法发送

    如果浏览器已经有同名的cookie那么新cookie会覆盖旧cookie的值

## 获取Cookie信息

* `String getName()`

    获取Cookie名称

* `String getValue()`

    获取Cookie值

* `int getMaxAge()`

    获取Cookie最大有效时间(单位是秒)

## 设置Cookie

* `void setValue(String newValue)`

    设置该cookie的新值

* `void setMaxAge(int expiry)`

    设置该cookie在浏览器的最大存活时间，如果不设置默认为-1(即会话结束就销毁)

    当设置为0是，表示立即销毁

# HttpSession

用于跟踪用户状态，保证在用户在一个浏览器的不同页面能访问相同的资源

基于cookie保证一个浏览器只有一个会话对象

是域对象

## 获取session信息

* `long getCreationTime()`

    获取创建session的时间

* `String getId()`

    获取session的唯一ID

* `long getLastAccessedTime()`

    获取客户端上一次发送与此session关联的请求时间

* `int getMaxInactionInterval()`

    获取session不活跃失效时间

## 操作session

* `void invalidate()`

    销毁session

* `void setMaxInactiveInterval(int interval)`

    指定在无任何操作下，session失效的时间，单位为秒，负数表示session永不失效，默认为30分钟

## 获取其他域对象

* `ServletContext getServletContext()`

# ServletContext

上下文对象，或者叫全局作用域对象

web服务启动时创建，关闭时销毁

为所有web应用提供公共区域

## 获取方式

* GenericServlet
* ServletConfig
* HttpSession
* HttpServletReqeust



## 方法













# Listener

是Javaweb三大组件之一的监听器

用于监听web应用中三大域对象、信息的创建、销毁、增加，修改，删除等动作的发生，然后作出相应的响应处理。

服务器通过监听器创建event对象，可以通过该对象获得监听器对应的域对象或者属性名和属性值

## 监听ServletContext全局作用域

* 生命周期监听：`ServletContextListener`接口

    * `void contextInitialized(ServletContextEvent sce)`

        全局作用域创建时，服务器会自动调用该方法

    * `void contextDestroyed(ServletContextEvent sce)`

        全局作用域销毁时，服务器会自动调用该方法

* 属性监听：`ServletContextAttributeListenter`接口

    * `void attributeAdded(ServletContextAttributeEvent event)`

        添加属性时调用

    * `void attributeReplaced(ServletContextAttributeEvent event)`

        修改属性时条用

    * `void attributeRemoved(ServletContextAttributeEvent event)`

        删除属性时调用

## 监听session域

* 生命周期监听`HttpSessionListener`

    * `void sesionCreated(HttpSessionEvent se)`

        创建session时

    * `void sessionDestroyed(HttpSessionEvent se)`

        销毁session时

* 属性监听器`HttpSessionAttributeListener`

    * `void attributeAdded(HttpSessionBindingEvent event)`

        添加属性时

    * `void attributeReplaced(HttpSessionBindingEvent event)`

        修改属性时

    * `void attributeRemoved(HttpSessionBindingEvent event)`、

        移除属性时

## 监听request域

* 生命周期监听`ServletRequestListener`

    * `void requestinitialized(servletRequestEvent sre)`

        创建request时

    * `void requestDestroyed(ServletRequestEvent sre)`

        销毁request时

* 属性监听`ServletRequestAttributeListener`

    * `void attributeAdded(ServletRequestAttributeEvent srae)`

        添加属性时

    * `void attributeReplaced(ServletRequestAttributeEvent srae)`

        修改属性时

    * `void attributeRemoved(ServletRequestAttributeEvent srae)`

        移除属性时

# Filter

Javaweb三大组件中的过滤器

用于过滤请求

## Filter接口方法

* `void init(FilterConfig filterConfig)`

    过滤器初始化方法

* `void doFilter(ServletRequest servletRequest,ServletResponse servletResponse,FilterChain filterChain)`

    过滤方法，拦截请求，将web.xml配置的相关请求拦截，

    * 调用FileChain中的doFilter方法放行请求
    * 如果不调用该方法则拦截请求

* `void destroy()`

    过滤器销毁方法

# web.xml文件的配置

web.xml文件是服务器的核心配置文件，主要配置javaweb的三大组件

服务器在启动时会读取web.xml文件中的内容

一旦web.xml配置信息有误，服务器就会启动失败

该文件需要：

1. 不能有重名

2. url-pattern：必须写/

3. 配置初始化参数

4. 设置组件启动时机 load-on-startup   **?**

## 配置Servlet

告诉服务器外界应该通过什么url路径访问Servlet组件

~~~xml
    <!--配置servlet资源路径并起别名 -->
	<servlet>
        <servlet-name>first</servlet-name>
        <servlet-class>com.bjpn.servlet.FirstServlet</servlet-class>
    </servlet>
    <!--配置servlet的请求映射   -->
    <servlet-mapping>
        <servlet-name>first</servlet-name>
        <url-pattern>/aaa</url-pattern>
    </servlet-mapping>
~~~

**注意：**url-pattern代表客户端访问路径，在这里必须写带`/`的相对路径

`/`代表服务器的根路径

## 配置Listener

服务器通过xml文件读取监听器，并自动开启监听

~~~xml
<listener>
	<listener-class>com.bjpn.listeners.AppListeners</listener-class>
</listener>
~~~

## 配置Filter

指定filter拦截请求的范围

~~~xml
<!--配置过滤器的请求-->
    <filter>
        <filter-name>ecodFilter</filter-name>
        <filter-class>com.bjpn.filters.EncodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>ecodFilter</filter-name>
        <!--配置过滤器的拦截范围
        /*:根目录下所有请求都拦截
        /*.do:所有带有.do的请求都拦截
        /*.jsp
        -->
        <url-pattern>/*</url-pattern>
        <dispatcher>REQUEST</dispatcher>
        <!--dispatcher配置拦截方式：
            REQUEST:当前过滤器拦截直接请求
            FORWARD:当前过滤器拦截转发请求
            INCLUDE:当前过滤器拦截包含请求
            ERROR:当前过滤器拦截错误请求
        -->
    </filter-mapping>
~~~

## 配置初始化参数

可以在`<servlet>`和`<filter>`标签中配置`<init-param>`标签以配置servlet和filter的初始化参数，该参数由servlet和filter的init初始化方法接收

~~~xml
<init-param>
    <param-name>name</param-name>
    <param-value>value</param-value>
</init-param>
~~~

# 域对象

### 域方法

servlet的域对象都有以下方法：

* `void setAttribute(String name,Object value)`

    设置域键值

* `Object getAttribute(String name)`

    获取指定域值

* `void removeAttribute(String name)`

    删除指定属性

* `Enumeration getAttributeNames()`

    获取所有属性名

# Servlet3.0的注解配置

## @Webservlet

替代web.xml中的sevlet配置

注解配置采用`属性名=值`的形式

| 属性名           | 类型              | 作用              | 等价于              |
| ---------------- | ----------------- | ----------------- | ------------------- |
| `name`           | `String`          | name属性          | `<servlet-name>`    |
| `value`          | `String[]`        | 等价于urlPatterns | `<url-pattern>`     |
| `urlPatterns`    | `String[]`        | URL匹配模式       | `<url-pattern>`     |
| `loadOnStartup`  | `int`             | 加载顺序          | `<load-on-startup>` |
| `initParams`     | `WebInitParame[]` | 初始化参数        | `<init-param>`      |
| `asyncSupported` | `boolean`         | 异步操作          | `<async-supported>` |
| `description`    | `String`          | 描述信息          | `<description>`     |
| `displayName`    | `String`          | 显示名            | `<idsplay-name>`    |

演示

~~~java
//name:别名
//value==urlPatterns 这是请求路径  可以是一个字符串  也可以是一个字符串数组
//initParams  初始化参数
//loadOnStartup 创建时机
//@WebServlet(name="second",value ="/secondDemo.action")
//@WebServlet(name="second",value ={"/secondDemo.action","/twoDemo.do"})
/*@WebServlet(name="second",urlPatterns ={"/secondDemo.action","/twoDemo.do"},
        initParams = {
                @WebInitParam(name="aaa",value = "AAA"),
                @WebInitParam(name="bbb",value = "BBB")
        },loadOnStartup = 1)*/
//日常工作中 我们不用再定义别名了
//如果是一个请求   可以省略value
@WebServlet("/secondDemo.action")
public class SecondServlet extends HttpServlet {
~~~

## @WebFilter

替代web.xml中的filter配置

有以下属性

| 属性名           | 类型              | 作用                | 等价于              |
| ---------------- | ----------------- | ------------------- | ------------------- |
| `filtername`     | `String`          | name属性            | `<filter-name>`     |
| `value`          | `String[]`        | 等价于urlPatterns   | `<url-pattern>`     |
| `urlPatterns`    | `String[]`        | URL匹配模式         | `<url-pattern>`     |
| `ServletNames`   | `String[]`        | 过滤器应用的servlet | `<servlet-name>`    |
| `dispatcherType` | `DispatcherType`  | 过滤器的转发模式    | `<dispatcher>`      |
| `initParams`     | `WebInitParame[]` | 初始化参数          | `<init-param>`      |
| `asyncSupported` | `boolean`         | 异步操作            | `<async-supported>` |
| `description`    | `String`          | 描述信息            | `<description>`     |
| `displayName`    | `String`          | 显示名              | `<idsplay-name>`    |

演示

~~~java
//如果只有一个value  可以省略value不写
//@WebFilter("/*")
@WebFilter(filterName = "/secondF",value = {"/*.jsp","/login/*.action"},
    initParams = {
        @WebInitParam(name="ccc",value = "CCC")
    }
)
public class SecondFilter implements Filter {
~~~

## @WebListener

替代web.xml中的listener配置

演示

~~~java
@WebListener
public class AttrListener implements HttpSessionAttributeListener {
~~~

# 文件上传

## 文件上传三要素

* 依赖包：`commons-fileupload.jar`,`commons-io.jar`
* 前端请求格式：`method="post"`,`enctype="multipart/form-data"`
* servlet配置：需要添加注解`@MultipartConfig`以开启识别Multipart数据结构的配置

## Part

是封装http文件上传的api接口

可通过HttpServletRequest的方法获取：

* `Part getPart(String name)`: 用于获取请求中指定name的文件
* `Coolection< Part > getParts()`;获取请求中全部的文件

方法：

* `void write(String fileName)`

    将文件内容写入指定磁盘位置

* `long getSize()`

    获取上传文件大小

* `String getName()`

    获取文件在表单中的name

* `String getHeader(String name)`

    获取指定的请求头

* `Collection<String> getHeaderNames()`

    获取所有请求头名称

* `Collection<String> getHeaders(String name)`

    获取指定请求头的集合数据

* `String getContentType()`

    获取文件MIME类型

* `inputStream getInputStream()`

    获取文件的输入流

* `void delete()`

    删除Part数据和临时目录数据，默认会删除

* `String getSubmittedFileName()`

    获取上传的文件名

## 上传文件模板

### 单文件上传

* 前端

~~~jsp
<form action="${pageContext.request.contextPath}/fileUpload.action" method="post" enctype="multipart/form-data">
    上传文件：<input type="file" name="file"><br/>
    <input type="submit">
</form>
~~~

* 后端

~~~java
@WebServlet("/fileUpload.action")
@MultipartConfig
public class FileUploadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Part file = req.getPart("file");
        //获取原文件名
        String oldFilename = file.getSubmittedFileName();
        //获取文件类型(扩展名)
        String extension = oldFilename.substring(oldFilename.lastIndexOf("."));
        //用时间戳作为文件主名
        Random random = new Random();
        String principal = System.currentTimeMillis()+"";
        //获得文件名
        String filename = principal +extension;
        //获取项目中保存该文件的位置
        //注意：需要将idea的output路径改为指向web文件夹(idea默认指向out文件夹)
        // 否则获取的真实路径是不正确的
        String path = req.getServletContext().getRealPath("/fileupload");
        System.out.println(path);
        //保存文件到项目web文件夹的fileupload下
        file.write(path+"/"+filename);
        System.out.println("上传成功");
    }
}
~~~

![](../img/output路径.png)

### 多文件上传

* 前端

~~~jsp
<form action="${pageContext.request.contextPath}/fileUpload.action" method="post" enctype="multipart/form-data">
    姓名：<input type="text" name="name"><br/>
    上传文件：<input type="file" name="file"><br/>
    上传文件：<input type="file" name="file"><br/>
    上传文件：<input type="file" name="file"><br/>
    <input type="submit">
</form>
~~~

* 后端

~~~java
@WebServlet("/fileUpload.action")
@MultipartConfig
public class FileUploadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //getParts()方法获取所有的请求属性，包括非文件，所以要判断part是否是文件类型，并判断是否是空文件
        Collection<Part> parts = req.getParts();
        for(Part part:parts){
            String olfFilename = part.getSubmittedFileName();
            if(olfFilename != null && !"".equals(olfFilename)){
                //获取文件名和后缀
                String oldFilename = part.getSubmittedFileName();
                String extension = oldFilename.substring(oldFilename.lastIndexOf("."));
                String principal = UUID.randomUUID().toString().replace("-","");
                String filename = principal +extension;
                //获取路径
                String path = req.getServletContext().getRealPath("/fileupload");
                System.out.println(path);
                part.write(path+"/"+filename);
            }
        }
        System.out.println("上传成功");
    }
}
~~~

# 文件下载

## 前提

需要设置响应头

告诉浏览器用用下载器来接受servlet传输的文件

~~~java
response.setHeader("content-disposition","attachment;filename=" + URLEncoder.encode(fileName, "UTF-8"));
~~~

## 模板

* 前端

~~~jsp
<a href="${pageContext.request.contextPath}/fileDownload.action？filename=1653817149862.jpg">下载文件</a>
~~~

* 后端

~~~java
@WebServlet("/fileDownload.action")
public class FileDownloadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取要下载的文件对象
        String filename = req.getParameter("filename");
        String path = req.getServletContext().getRealPath("/fileupload");
        File file = new File(path +"/"+filename);
        //获取下载到浏览器的文件名principal
        String principal = UUID.randomUUID().toString().replace("-","");
        String extension =filename.substring(filename.lastIndexOf("."));
        String newFilename = principal + extension;
        //设置响应头
        resp.setHeader("content-disposition","attachment;filename=" + URLEncoder.encode(newFilename, "UTF-8"));
        //获取输入输出流
        FileInputStream input = new FileInputStream(file);
        ServletOutputStream output = resp.getOutputStream();
        //写出文件
        byte[] bytes = new byte[1024];
        int len = 0;
        while((len = input.read(bytes))!= -1){
            output.write(bytes, 0, len);
        }
        System.out.println("下载成功");
    }
}
~~~

































