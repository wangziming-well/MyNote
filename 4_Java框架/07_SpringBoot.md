# springboot简介

SpringBoot是Spring家族中的一员，它是用来简化Spring应用程序的创建和开发过程。

它通过采用大量默认配置的方式简化之前框架中繁琐配置

它还可以集成许多优秀的框架

## 特性

* 快速创建基于Spring的应用程序
* 直接使用java main方法启动内嵌的Tomcat服务器运行Spring Boot程序，不需要部署war包
* 提供约定的starter POM来简化Maven配置
* 采用注解配置，Java配置来替代了XML文件配置

## 核心

* 自动配置：针对很多Spring应用程序和常见的应用功能，Spring Boot能自动提供相关配置
* 起步依赖：告诉Spring Boot需要什么功能模块，它能够引入需要的依赖库
* Actuator：让你能够深入运行中的Spring Boot应用程序，一探Spring Boot程序的内部信息
* 命令行界面：这是Spring Boot的可选特性，主要针对Groovy语言使用



# SpringBoot Web项目结构

* `.mvn|mvnw|mvnw.cmd`使用脚本操作执行maven相关命令，国内使用较少，可删除

* `src`

    * `main`

        * `java`

            * `com`

                * `bjpn`

                    * `springbootdemo`

                        * `SpringBootDemoApplication.java`

                            SpringBoot程序执行的入口，执行该程序中的main方法，SpringBoot就启动了，自动启动内置tomcat运行

        * `resources`

            * `static`放一些静态内容 css js img

            * `templates`基于模板的html

            * `application.properties`

                SpringBoot的配置文件，很多集成的配置都可以在该文件中进行配置，例如：Spring、springMVC、Mybatis、Redis等。目前是空的

* `.gitignore`使用版本控制工具git的时候，设置一些忽略提交的内容V

* `pom.xml`maven工程的配置文件

## springboot的pom文件

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!--继承SpringBoot框架的一个父项目，所有自己开发的Spring Boot都必须的继承-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.1</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <!--当前项目的GAV坐标-->
    <groupId>com.bjpn</groupId>
    <artifactId>SpringBootDemo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <!--maven项目名称，可以删除-->
    <name>SpringBootDemo</name>
    <!--maven项目描述，可以删除-->
    <description>SpringBootDemo</description>
    <!--maven属性配置，可以在其它地方通过${}方式进行引用-->
    <properties>
        <java.version>11</java.version>
    </properties>
    <dependencies>
        <!--SpringBoot框架web项目起步依赖，通过该依赖自动关联其它依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--SpringBoot框架的测试起步依赖，可以删除-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--热部署插件，可在创建项目时勾选-->
        <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-devtools</artifactId>
           <optional>true</optional>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!--SpringBoot提供的打包编译等插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
~~~

## SpringBoot程序执行的入口

可以在该程序入口获取spring上下文对象，执行非web应用：

~~~java
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class Application {
    
    public static void main(String[] args) {
        /*
         SpringBoot程序启动后，返回值是ConfigurableApplicationContext
         它也是一个Spring容器对象
         相当于原来Spring中启动容器ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("");
         */
        //获取SpringBoot程序启动后的Spring容器
        ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);
        //从Spring容器中获取指定bean的对象
        UserService userService = (UserService) context.getBean("userServiceImpl");
        //调用业务bean的方法
        String sayHello = userService.sayHello();
        System.out.println(sayHello);
    }
}
~~~

也可以在这里设置日志的输出：

~~~java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication springApplication = new SpringApplication(Application.class);
        //关闭启动logo和启动日志的输出
        springApplication.setBannerMode(Banner.Mode.OFF);
        springApplication.run(args);
    }
}
~~~

**tips:**

在src/main/resources放入banner.txt文件，该文件名字不能随意，文件中的内容就是要输出的logo

## springboot项目解释

* Spring Boot的父级依赖spring-boot-starter-parent配置之后，当前的项目就是Spring Boot项目

* spring-boot-starter-parent是一个Springboot的父级依赖，开发SpringBoot程序都需要继承该父级项目，它用来提供相关的Maven默认依赖，使用它之后，常用的jar包依赖可以省去version配置

* Spring Boot提供了哪些默认jar包的依赖，可查看该父级依赖的pom文件

* 如果不想使用某个默认的依赖版本，可以通过pom.xml文件的属性配置覆盖各个依赖项，比如覆盖Spring版本

    ~~~xml
    <properties>
        <spring.version>5.0.0.RELEASE</spring.version>
    </properties>
    ~~~

* `@SpringBootApplication`注解是Spring Boot项目的核心注解，主要作用是开启Spring自动配置，如果在Application类上去掉该注解，那么不会启动SpringBoot程序

# SpringBoot核心配置文件

Spring Boot 的核心配置文件用于配置Spring Boot 程序，名字必须以application开始

提供了两种配置文件格式：`application.properties`和`application.yml`

默认使用`.properties`的配置

* `application.properties`

    采用键值对进行配置

~~~properties
#设置内嵌Tomcat端口号
server.port=9090
#配置项目上下文根
server.servlet.context-path=/SprintBootDemo
~~~

* `application.yml`

    主要采用一定的空格、换行等格式排版进行配置。

~~~yml
server:
	port: 9090
	servlet:
		context-path: /SprintBootDemo
~~~

## 多环境配置

在实际开发过程中，项目会经过多个阶段（开发，测试，上线），每个阶段的环境配置也会不同，例如：端口、上下文、数据库

为了方便在不同环境之间切换，springBoot提供了多环节配置

接下来以`.properties`为例，(yaml文件同理)

配置多个application配置文件

* `resources`
    * `application.properties`
    * `application-dev.properties`
    * `application-product.properties`
    * `application-test.properties`

然后在`application.properties`文件中配置属性以激活环境：

~~~properties
spring.profiles.active=dev|product|test
~~~

**等号右边的值和配置文件的环境标识名一致**

被激活的配置文件会覆盖`application.properties`文件：

* 如果`application.properties`和激活的配置文件中都有相同的配置，那么会采用激活的配置文件中的配置

## 自定义配置

在SpringBoot的核心配置文件中，除了使用内置的配置项以外，还可以自定义配置，然后采用注解的方式读取配置的属性值

以下面的自定义配置为例：

~~~yml
school:
	name: bjpowernode
	websit: www.bjpowernode.com
~~~

# Springboot的Java配置

Springboot不建议使用xml配置文件

可以通过Java注解和类的方式进行自定义配置

比较常用的注解有：

- `@Configuration`：声明一个类作为配置类，代替xml文件

- `@Bean`：声明在方法上，将方法的返回值加入Bean容器，代替`<bean>`标签

    主要用在@Configuration注解的类里，也可以用在@Component注解的类里

    添加的bean的id为方法名

- `@Value`：注入属性在声明的属性上使用`@Value`注解，springboot将自动把配置值赋给该属性

- `@ConfigurationProperties`

    可以将配置的所有子配置映射成一个对象，用于自定义配置项比较多的情况

    指定在类上使用@ConfigurationProperties并指定prefix属性，springboot会根据prefix指定的配置，寻找该配置下的所有子配置，并将这些子配置赋值给类中具有相同名称的属性

    prefix可以不指定，如果不指定，那么会去配置文件中寻找与该类的属性名一致的配置

- `@PropertySource`：指定外部属性文件

**注意：**

1. 如果类上没有指定@PropertySource；那么这个类中的@Value注解将在默认的配置文件中寻找匹配的属性、

2. 解决使用@ConfigurationProperties注解出现警告问题

~~~xml
<!--解决使用@ConfigurationProperties注解出现警告问题-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
~~~

# 在springboot中使用JSP

springboot不建议使用jsp技术，更建议使用模板技术

## 依赖

~~~xml
<!--引入Spring Boot内嵌的Tomcat对JSP的解析包，不加解析不了jsp页面-->
<!--如果只是使用JSP页面，可以只添加该依赖-->
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
</dependency>

<!--如果要使用servlet必须添加该以下两个依赖-->
<!-- servlet依赖的jar包-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
</dependency>

<!-- jsp依赖jar包-->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>javax.servlet.jsp-api</artifactId>
    <version>2.3.1</version>
</dependency>

<!--如果使用JSTL必须添加该依赖-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
</dependency>

~~~

## 配置资源扫描

SpringBoot要求jsp文件必须编译到指定的META-INF/resources目录下才能访问，否则访问不到。

~~~xml
<!--
    SpringBoot要求jsp文件必须编译到指定的META-INF/resources目录下才能访问，否则访问不到。
    其它官方已经建议使用模版技术（后面会课程会单独讲解模版技术）
-->
<resources>
    <resource>
        <!--源文件位置-->
        <directory>src/main/webapp</directory>
        <!--指定编译到META-INF/resource，该目录不能随便写-->
        <targetPath>META-INF/resources</targetPath>
        <!--指定要把哪些文件编译进去，**表示webapp目录及子目录，*.*表示所有文件-->
        <includes>
            <include>**/*.jsp</include>
        </includes>
    </resource>
</resources>
~~~

# Springboot使用Servlet组件

spring中springmvc封装了servlet，在springboot中没有提供接口直接直接使用servlet，不过可以通过注解和配置的方式来使用它们

## 注解扫描

`@ServletComponentScan(basePackages = "")`

在springboot程序执行入口类上声明上该注解，将自动扫描注册指定包下的servlet组件

## Java配置

可以通过Java配置的方式手动注册Servlet组件

springboot提供了servlet组件的注册类，以供我们使用Java配置的方式注册它们：

* ServletRegistrationBean
* ServletListenerRegistrationBean

* FilterRegistrationBean

将以上类的实例交给spring管理（在配置类中，@Bean声明的方法中返回以上类的实例）

在创建以上类的实例时，需要通过它们的构造函数将servlet组件的实例传入，并传入必要的参数(通过构造方法或者对象方法)，如url等

示例：

~~~java
@Configuration 
public class ServletConfig {
    @Bean
    public ServletRegistrationBean<HttpServlet> heServletRegistrationBean() {
        return new ServletRegistrationBean<>(new MyServlet(),"/myServlet");
    }
}
~~~

```java
@Configuration
public class FilterConfig {
    @Bean
    public FilterRegistrationBean<Filter> myFilter(){
        FilterRegistrationBean<Filter> filterRegistrationBean = new FilterRegistrationBean<>(new MyFilter());
        filterRegistrationBean.addUrlPatterns("/*");
        return filterRegistrationBean;
    }
}
```

```java
@Configuration
public class ListenerConfig {
    @Bean
    public ServletListenerRegistrationBean<EventListener> myListener(){
        return new ServletListenerRegistrationBean<>(new MyListener());
    }
}
```

# Springboot使用Actuator

Actuator是Spring Boot提供的对应用系统的自省和监控的集成功能，可以对应用系统进行配置查看、健康检查、相关功能统计等

## 依赖

~~~xml
<!--Spring Boot Actuator依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
~~~

## 配置

~~~yaml
management:
    server:
        #actuator监控的端口（端口可配可不配，如果不配置，则使用和server.port相同的端口）
        port: 8080
        #actuator监控的访问上下文根路径（路径可配可不配，如果不配置，则使用和server.context-path相同的路径）
        base-path: /actuator
        endpoints:
            web:
                exposure:
                    #默认只开启了health和info，设置为*，则包含所有的web入口端点
                    include: *
~~~

## 使用

| **HTTP****方法** | **路径**        | **描述**                                   |
| ---------------- | --------------- | ------------------------------------------ |
| GET              | /configprops    | 查看配置属性，包括默认配置                 |
| GET              | /beans          | 查看Spring容器目前初始化的bean及其关系列表 |
| GET              | /env            | 查看所有环境变量                           |
| GET              | /mappings       | 查看所有url映射                            |
| GET              | /health         | 查看应用健康指标                           |
| GET              | /info           | 查看应用信息                               |
| GET              | /metrics        | 查看应用基本指标                           |
| GET              | /metrics/{name} | 查看具体指标                               |
| JMX              | /shutdown       | 关闭应用                                   |

# Springboot程序的打包部署

## 打包

* 如果要打war包，程序入口类需扩展继承 SpringBootServletInitializer类并覆盖configure方法

~~~java
@SpringBootApplication
public class Application extends SpringBootServletInitializer{
   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }
   @Override
   protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
//参数为当前Spring Boot启动类Application.class
      return builder.sources(Application.class);
   }
}
~~~

* 配置pom文件

~~~xml
<!--打包方式-->
<packaging>war|jar</packaging>

<build>
    <!--指定包名-->
	<finalName>packageName</finalName>
</build>
<!--SpringBoot 的打包插件(默认自动添加)-->
<plugin>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>

~~~

* 打包：通过Maven package命令打war包到target目录下

## 部署

* war包：将war包拷贝到tomcat的webapps目录，并启动tomcat
* jar包：通过java命令执行jar包  `java -jar 包名`
