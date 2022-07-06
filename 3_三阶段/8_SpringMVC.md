# SpringMVC介绍

* 是一个控制层框架，封装了servlet
* 时Spring框架的一部分

## SpringMVC执行流程

1. 用户发送请求到前端控制器（DispatcherServlet）。

2. 前端控制器请求处理器映射器（HandlerMapping）去查找处理器（Handler）。

3. 找到以后处理器映射器（HandlerMappering）向前端控制器返回执行链（HandlerExecutionChain）。

4. 前端控制器（DispatcherServlet）调用处理器适配器（HandlerAdapter）去执行处理器（Handler）。

5. 处理器适配器去执行Handler。

6. 处理器执行完给处理器适配器返回ModelAndView。

7. 处理器适配器向前端控制器返回ModelAndView。

8. 前端控制器请求视图解析器（ViewResolver）去进行视图解析。

9. 视图解析器向前端控制器返回View。

10. 前端控制器对视图进行渲染。

11. 前端控制器向用户响应结果。

![](../img/SpringMVC执行流程.png)



## 环境搭建

* maven依赖

    ~~~xml
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.3.RELEASE</version>
    </dependency>
    ~~~

* web.xml文件头约束的版本高于2.5

    ~~~xml
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns="http://xmlns.jcp.org/xml/ns/javaee"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
             id="WebApp_ID" version="4.0">
    
    </web-app>
    ~~~

* 在web.xml文件配置中央控制器servlet

    ~~~xml
    <!--配置DispatcherServlet -->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--将springmvc核心配置文件作为初始化参数传入dispatcherServlet
     		前端控制器会读取配置文件并根据文件创建三大对象：
    		处理器映射器，处理器适配器，视图解析器
    	-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--保证前端控制器第一时间启动 -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <!--前端控制器的请求
          第一种：/  代表过滤所有
          第二种:*.action   *.do   *.jsp    配置具体的后缀
        -->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    ~~~

# 核心配置文件

文件头约束

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
  http://www.springframework.org/schema/context
  http://www.springframework.org/schema/context/spring-context-3.1.xsd
  http://www.springframework.org/schema/mvc
  http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd">
    
</beans>
~~~



## 非注解版(了解)

* springmvc.xml

~~~xml
<!--手动配置三大适配器-->
<!--处理器映射器-->
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
<!--处理器适配器-->
<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
<!--视图解析器-->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"/>

<!--处理器-->
<bean id="/firstController" class="com.bjpn.FirstController"/>
~~~

* controller

~~~java
public class FirstController implements Controller {
    @Override
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView mav = new ModelAndView();
        System.out.println("这是我的第一个处理器");
        return null;
    }
}
~~~

## 注解版

* springmvc.xml

~~~xml
<!--使用注解  简化配置  和SpringMVC的使用-->
<!--自动扫描   三大件   处理器映射器  处理器适配器  视图解析器-->
<mvc:annotation-driven/>
<!--处理器  注解扫描   自动扫描 @Controller-->
<context:component-scan base-package="com.bjpn.controllers"/>
~~~

* controller

~~~java
@Controller
public class SecondController {
    @RequestMapping("/secondController.action")
    public String controller(){
        return "/index.jsp";
    }
}
~~~



# SpringMVC常用注解

* `@Controller`标识当前类是处理器类

* `@RequestMapping`映射url路径，可以出现在类和方法上

    在类上表示当前处理方法的父路径，在方法上表示当前处理方法的路径

    参数：

    * value:表示请求路径，值为路径字符串数组
    * method:表示请求方式，只能在方法上时用，如GET，POST

* `@PathVariable`接收动态参数  参数值写在请求中
* `@requestParam`         配置不同名参数
* `@ResponseBody`     异步ajax的json格式
* `@RequestBody`      接收前端异步请求参数

# SpringMVC处理器

表示处理器的方法有三种，分别是返回值为：

* `ModelAndView`返回视图，渲染后响应跳转页面资源显示给用户
* `String`返回要跳转的页面路径字符串，工作中常用
* `void`不跳转页面，常用于简单的异步

演示：

~~~java
@Controller
public class SecondController {
    @RequestMapping("/methodDemo1.action")
    public String methodDemo1(){
        return "/index.jsp";
    }
    @RequestMapping("/methodDemo2.action")
    public ModelAndView methodDemo2(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("/index.jsp");
        return modelAndView;
    }
    @RequestMapping("/methodDemo3.action")
    public void methodDemo3(HttpServletRequest request, HttpServletResponse response) throws IOException {
        PrintWriter writer = response.getWriter();
        writer.write("响应成功");
    }
}
~~~



## 转发与重定向

SpringMVC处理器，不管返回值是ModelAndView还是String，默认调用转发

可以通过在表示资源路径的字符串中指定跳转类型来指定跳转方式：

* forward：表示转发
* redirect：表示重定向

演示：

~~~java
@Controller
public class ThirdController {
    @RequestMapping("/jumpByForward.action")
    public ModelAndView jumpByForward(){
        ModelAndView modelAndView = new ModelAndView();
        modelAndView.setViewName("forward:/index.jsp");
        return modelAndView;
    }
    @RequestMapping("/jumpByRedirect.action")
    public String jumpByRedirect(){
        return "redirect:/index.jsp";
    }
}
~~~



# SpringMVC处理器适配器

处理器适配器封装了从前端接受参数的过程，以及创建对象的过程

处理器适配器能给对应的处理器提供

* 当前工程中的对象
* 前端传递的参数

## 提供对象

适配器能为处理器提供当前工程中所有的有无参构造的类对象，

只需要处理器在形参列表中声明：

示例：

~~~java
@RequestMapping("objectSupport.action")
public ModelAndView objectSupport(ModelAndView modelAndView , User user){
    modelAndView.setViewName("redirect:/main.jsp");
    System.out.println(user);
    return modelAndView;
}
~~~



## 提供参数

适配器可以给处理器提供前端传递的参数，处理器可以用多种方式接收参数

### 通过同名参数接收

适配器会将前端的参数传递给与处理器形参名相同的位置，并自动进行类型转换

示例：

前端：

~~~jsp
 <a href="${pageContext.request.contextPath}/demo/getParamDemo1.action?name=张三&age=18">通过同名参数接收参数</a>
~~~

处理器：

~~~java
@RequestMapping("/getParamDemo1.action")
public void getParamDemo1(String name ,int age){
    System.out.println("name:"+name +"---age:"+(age+2));
}
~~~

### 通过对象接收

适配器会扫描处理器形参上的对象属性，如果前端参数与属性名相同，也会自动将参数值赋值给对象

前端：

~~~jsp
<a href="${pageContext.request.contextPath}/demo/getParamDemo2.action?name=张三">通过对象接收参数</a>
~~~

处理器：

~~~java
@RequestMapping("/getParamDemo2.action")
public void getParamDemo2(User user){
    System.out.println(user);
}
~~~

### 通过不同名对象接收

可以通过`@RequestParam`注解，指定处理器形参要接收的参数名

前端：

~~~jsp
<a href="${pageContext.request.contextPath}/demo/getParamDemo3.action?name=张三">接收不同名参数</a>
~~~

处理器：

~~~java
@RequestMapping("/getParamDemo3.action")
public void getParamDemo3(@RequestParam("name") String uname){
    System.out.println("uname:"+uname);
}
~~~

### restful风格接收

可以直接将请求写在参数中，接收请求参数需要在请求路径中用`{}`且需要在要接收该参数的形参位置加上注解`@PathVariable()`

springmvc在接收到前端请求后，会先扫描一般请求路径，如果没有匹配的，再匹配restful风格的请求路径，如果格式匹配，则会分发给对应处理器

前端：

~~~jsp
<a href="${pageContext.request.contextPath}/demo/张三.action">restful风格接收参数</a>
~~~

后端：

~~~java
@RequestMapping("/{name}.action")
public void getParamDemo4(@PathVariable("name") String name){
    System.out.println(name);
}
~~~



# SpringMVC提供的域对象

在servlet中我们使用request，session，servletContext(application)域对象来向前端传递参数

在SpringMVC中：

* request，session对象可以由处理器适配器直接提供给处理器

* servletContext对象因为没有无参构造，所以只能由servlet-api中的方法获取

除此之外SpringMVC还自己封装了域对象，以供传值：

## ModelAndView

ModelAndView除了提供视图外，还能够起到域对象的作用

生命周期与request相同，但是在重定向时，modelAndView会将key-value拼接到请求中，多用于服务器内跳转

示例：

~~~java
//ModelAndView  转发时类似request域
@RequestMapping("/returnParamDemo3.action")
public ModelAndView returnParamDemo3(ModelAndView modelAndView){
    modelAndView.addObject("mavKey","这是mav传值");
    modelAndView.setViewName("forward:/page/paramSuccess.jsp");
    return modelAndView;
}
//ModelAndView  重定向时会把key-value拼接在请求中  多用在跳转其它处理器
@RequestMapping("/returnParamDemo4.action")
public ModelAndView returnParamDemo4(ModelAndView modelAndView){
    modelAndView.addObject("mavKey","这是mav传值");
    modelAndView.setViewName("redirect:/page/paramSuccess.jsp");
    return modelAndView;
}
~~~

## Model

与ModelAndView类似，为了在String返回值类型的处理器中传值

示例：

~~~java
//使用Model
@RequestMapping("/returnParamDemo5.action")
public String returnParamDemo5(Model model){
    model.addAttribute("modelKey", "这是model传值");
    return "forward:/page/paramSuccess.jsp";
}
//重定向时会把key-value拼接在请求中  多用在跳转其它处理器
@RequestMapping("/returnParamDemo6.action")
public String returnParamDemo6(Model model){
    model.addAttribute("modelKey", "这是model传值");
    return "redirect:/page/paramSuccess.jsp";
}
~~~

# SpringMVC解决中文乱码问题

SpringMVC提供了编码过滤器，直接在web.xml中配置即可：

~~~xml
<!--解决post中文乱码问题-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <!--指定编码格式-->
    <init-param>
        <param-name>encoding</param-name>
        <param-value>utf-8</param-value>
    </init-param>
    <!--这两个可以不写-->
    <!--强制开启request字符集-->
    <init-param>
        <param-name>forceRequestEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
    <!--强制开启response字符集-->
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
~~~



# SpringMVC读取静态资源

在配置SpringMVC的中央控制器DispatcherServlet时，我们设置的url-pattern是`/`,这意味着浏览器的所有请求都会被中央控制器拦截处理，包括动态资源和静态资源的请求

但中央处理器只能处理类似.jsp .actiond 的动态资源，无法处理 .html .js .css 的静态资源，这导致了tomcat无法读取静态资源给浏览器

有三个方法方案：

1. 使用tomcat自带的default Servlet处理
2. 在SpringMVC中配置静态资源路径
3. 在SpringMVC中设置静态资源的处理方式：交给default Servlet



## 使用Defalut Servlet

直接在web.xml文件中配置默认servlet路径:

~~~xml
  <!--配置默认servlet-->
  <servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>/images/*</url-pattern>
    <url-pattern>/static/*</url-pattern>
    <url-pattern>/photo/*</url-pattern>
    <url-pattern>/laydate/*</url-pattern>
    <url-pattern>*.js</url-pattern>
    <url-pattern>*.css</url-pattern>
  </servlet-mapping>
~~~

tomcat会优先处理更具体精确的路径，所以tomcat收到请求后，会先匹配default的路径，如果是default路径指定的url pattern 则会交给default处理，如果在指定的路径范围，才会再交给DispatcherServlet处理



## 在SpringM配置静态资源路径

在SpringMVC的核心配置文件中：

~~~xml
<!-- 以下路径不会被当控制器拦截，当静态资源处理 -->
<mvc:resources mapping="/images/*" location="/images/" />
<mvc:resources mapping="/css/*" location="/css/" />
<mvc:resources mapping="/js/*" location="/js/" />
~~~



## SpringMVC交还给default Servlet处理

在SpringMVC核心配置文件中：

~~~xml
<!-- 由springmvc对请求进行分类，如果是静态资源，则交给DefaultServlet处理 -->
<mvc:default-servlet-handler/>
~~~



# Jackson处理异步数据

springMVC提供了jackson以处理json数据

* 引入依赖：

    需要导入core detabind annotations

    ~~~xml
    <!--导入jackson-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.9.0</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.0</version>
    </dependency>
    ~~~

* 注解`@ResponseBody`

    该注解可以在方法上和方法返回值上，可以自动将处理器返回值对象转换成json字符串，并响应给请求

    ~~~java
    @RequestMapping("/login.action")
    public @ResponseBody Admin login() throws IOException {
        Admin  admin= new Admin(1, "123", "123");
        return admin;
    }
    ~~~

    前端js：

    ~~~js
    $.post(rootPath+ "/admin/login.action" ,data,function(message){
        alert(message.number+"---"+message.username+"---"+message.password)
    })
    ~~~

可以通过这种方法来响应异步请求

* 注解`@RequestBody`(了解)

    在SpringMVC低版本时，接收前台传递的json数据时，必须在处理器的形参上加上该注解，而且形参必须不能是对象

    现在高版本，不需要该注解也可以进行json解析，并自动将参数值赋给对象属性

# 配置前置后置路径

​		如果直接将`.jsp`文件放在webapp文件夹下，用户就可以直接通过浏览器地址栏访问到它，这会造成安全风险；同时这样直接访问，请求不会走处理器映射器和处理器适配器，这意味着SpringMVC的拦截器不会对该资源生效。

​		为了避免这种情况，可以把`.jsp`文件放到WEB-INF下，WEB-INF不接受直接请求，然后让所有对`.jsp`页面的访问通过处理器转发到。这样用户就只能通过访问处理器，间接访问`.jsp`文件了。

为了方便我们设置处理器的跳转路径，我们可以设置视图解析器的前置后置路径，这样通过视图解析器访问的路径，会自动拼装设置的前缀后缀：

~~~xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/"/>
    <property name="suffix" value=".jsp"/>
</bean>
~~~

这样返回字符串或者ModelAndView对象的处理器，返回视图时，视图路径将自动拼装设置的前后缀：

~~~java
//index.jsp在项目下的路径为 webapp/WEB-INF/index.jsp
@RequestMapping("/toIndex.action")
public String toIndex(){
    return "index";
}
//该处理器返回的实际视图路径为 /WEB-INF/index.jsp
~~~

# 文件传输

## 文件上传

在`servlet-api`中，我们学习了文件上传的三要素：

* 依赖包：`commons-fileupload.jar`,`commons-io.jar`
* 前端请求格式：`method="post"`,`enctype="multipart/form-data"`
* servlet配置：需要添加注解`@MultipartConfig`以开启识别Multipart数据结构的配置

现在可以通过maven依赖导入依赖包：

~~~xml
<dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.1</version>
    </dependency>
~~~

在SpringMVC框架下，前两个要素不变，servlet 的文件传输配置由SpringMVC框架封装，只需要在核心配置文件中配置文件上传解析器：

**！！注意：**id必须是multipartResolver

~~~xml
<!--配置文件上传解析器-->
<!--id必须是multipartResolver-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <property name="maxUploadSize" value="#{1024*1024*80}"/>
    <property name="defaultEncoding" value="utf-8"/>
</bean>
~~~

SpringMVC还封装的servlet 的part对象，提供了MultipartFile文件对象

处理器可以直接通过处理器适配器获取该对象，可以通过该对象更方便地写出上传的文件

前端表单：

~~~html
<form id="file-upload">
    姓名：<input type="text" name="username"><br/>
    <input type="file" name="fileUpload"><br/>
    <input type="button" value="提交" id="submit">
</form>
~~~

js：

~~~js
$("#submit").click(function () {
    var data = new FormData();
    data.append("username",$("input[name='username']").val());
    data.append("fileUpload",$("input[name='fileUpload']")[0].files[0]);
    $.ajax({
        type:"post",
        url:"${pageContext.request.contextPath}/fileUpload.action",
        contentType:false,
        processData:false,
        enctype:"multipart/form-data",
        data:data,
        dataType:"json",
        success:function (message) {
            alert(message.messageStr)
        }
    })
})
~~~

处理器：

~~~java
// 文件上传处理器
@RequestMapping("/fileUpload.action")
@ResponseBody
public Message fileUpload(HttpServletRequest request, String username, MultipartFile fileUpload, Message message) throws IOException {
    System.out.println(username);
    String oldFileName = fileUpload.getOriginalFilename();
    String fileType = oldFileName.substring(oldFileName.lastIndexOf("."));
    String fileName = UUID.randomUUID().toString().replace("-","") +fileType;
    String path = request.getServletContext().getRealPath("/file");
    fileUpload.transferTo(new File(path + "/" + fileName));
    message.setMessageStr("上传成功");
    return message;
}
~~~

**注意：**用上下文获取真实路径时，需要更改项目的output directory到webapp下；

或者配置虚拟路径

## 文件下载

~~~java
@Controller
public class DownController {
    @RequestMapping("down")
    public ResponseEntity<byte[]> down() throws Exception{
        File file = new File("C:\\yf\\test.png");
        //设置响应头为下载
        HttpHeaders headers = new HttpHeaders();
        headers.setContentDispositionFormData("attachment",new String("测试下载.png".getBytes("GBK"),"ISO-8859-1"));
        byte[] bytes = FileUtils.readFileToByteArray(file);
        return new ResponseEntity<byte[]>(bytes, headers, HttpStatus.OK);
    }
}
~~~



# 拦截器

SpringMVC提供了类似Servlet的过滤器的拦截器，拦截器的作用时间在处理器适配器执行处理器之前

配置拦截器：

~~~xml
<!-- 拦截器配置 -->
<mvc:interceptors>
    <!-- 多个拦截器将顺序执行 -->
    <mvc:interceptor>
        <mvc:mapping path="/**"/> <!-- 拦截路径  **代表着多层路径 -->
        <!--<mvc:exclude-mapping path="/login"/>--><!-- 不拦截路径 -->
        <bean class="com.bjpn.inter.LoginInter"></bean>
    </mvc:interceptor>
</mvc:interceptors>
~~~

拦截器：

~~~java
public class LoginInter implements HandlerInterceptor {
    //访问前连接拦截  请求到达拦截器  判断请求是否合理  放行 true   不放行是false
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("这是访问前 ");
        StringBuffer path = request.getRequestURL();
        System.out.println("path:"+path);
        return false;
    }
    //访问后拦截
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        //处理器处理完毕  要返回值到前端控制器    可以进行拦截  还可以查看携带的值
    }
   //消亡
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}
~~~





