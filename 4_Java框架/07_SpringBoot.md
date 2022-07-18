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



## @Value

可以一次读取单个配置值

在声明的属性上使用`@Value`注解，springboot将自动把配置值赋给该属性

示例：

~~~java
@Controller
public class SpringBootController {

    @Value("${school.name}")
    private String schoolName;

    @Value("${school.websit}")
    private String schoolWebsit;

    @RequestMapping(value = "/springBoot/say")
    public @ResponseBody String say() {
        return schoolName + "------" + schoolWebsit;
    }
}

~~~

## @ConfigurationProperties

可以将配置的所有子配置映射成一个对象，用于自定义配置项比较多的情况

指定在类上使用@ConfigurationProperties并指定prefix属性，springboot会根据prefix指定的配置，寻找该配置下的所有子配置，并将这些子配置赋值给类中具有相同名称的属性

prefix可以不指定，如果不指定，那么会去配置文件中寻找与该类的属性名一致的配置

~~~java
@Component
@ConfigurationProperties(prefix = "school")
public class ConfigInfo {

    private String name;

    private String websit;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getWebsit() {
        return websit;
    }

    public void setWebsit(String websit) {
        this.websit = websit;
    }
}
~~~

注意：

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



# Springboot集成MyBatis

mybatis对spring进行了集成

## 依赖

~~~xml
<!--MyBatis整合SpringBoot的起步依赖-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.0.0</version>
</dependency>
<!--MySQL的驱动依赖-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
~~~

## 配置

springboot配置

~~~properties
#配置数据库的连接信息
#注意这里的驱动类有变化
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springboot?useUnicode=true&characterEncoding=utf8&useSSL=false
spring.datasource.username=root
spring.datasource.password=root
~~~

maven配置资源扫描

~~~xml
<resources>
    <resource>
        <directory>src/main/java</directory>
        <includes>
            <include>**/*.xml</include>
        </includes>
    </resource>
</resources>
~~~



## 注解

* `@Mapper`标记当前类为mapper类

* `@MapperScan("com.bjpn.springboot.mapper")`扫描mapper包的注解

    需要再运行主类Application上添加



## mapper配置文件

如果mapper.xml没有与接口放到一起放在mapper包下，而是放在resources下的mapper包中，那么需要再springboot配置中配置：

~~~properties
mybatis.mapper-locations=classpath:mapper/*.xml
~~~

## 事务

* 在入口类中使用注解 @EnableTransactionManagement 开启事务支持
* 在访问数据库的Service方法上添加注解 @Transactional 即可

@Transacitonal注解可以设置的参数：

*  propagation

    事务传播行为

    * REQUIRED：支持当前事务，如果当前没有事务，就新建一个事务。这是最常见的选择。 
    * SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行。 
    * MANDATORY：支持当前事务，如果当前没有事务，就抛出异常。 
    * REQUIRES_NEW：新建事务，如果当前存在事务，把当前事务挂起。 
    * NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。 
    * NEVER：以非事务方式执行，如果当前存在事务，则抛出异常。 
    * NESTED：支持当前事务，如果当前事务存在，则执行一个嵌套事务，如果当前没有事务，就新建一个事务。 

* timeout 超时时间，默认30秒

* isolation

    事务隔离级别

    MYSQL: 默认为REPEATABLE_READ级别
    SQLSERVER: 默认为READ_COMMITTED

    * Isolation.READ_UNCOMMITTED  : 读取未提交数据(会出现脏读, 不可重复读) 基本不使用

    * Isolation.READ_COMMITTED  : 读取已提交数据(会出现不可重复读和幻读)

    * Isolation.REPEATABLE_READ：可重复读(会出现幻读)
        Isolation.SERIALIZABLE：串行化

* readOnly 

    属性用于设置当前事务是否为只读事务，设置为true表示只读，false则表示可读写，默认值为false。

* rollbackFor
* 该属性用于设置需要进行回滚的异常类数组，当方法中抛出指定异常数组中的异常时，则进行事务回滚

*  rollbackForClassName

    该属性用于设置需要进行回滚的异常类名称数组，当方法中抛出指定异常名称数组中的异常时，则进行事务回滚

* noRollbackForClassName

    该属性用于设置不需要进行回滚的异常类名称数组，当方法中抛出指定异常名称数组中的异常时，不进行事务回滚

* noRollbackFor

    该属性用于设置不需要进行回滚的异常类数组，当方法中抛出指定异常数组中的异常时，不进行事务回滚

**注意：**以上四个rollbackFor参数，既可以指定单个参数，也可以用数组指定多个参数,例如：

指定单一异常类：@Transactional(noRollbackFor=RuntimeException.class)

指定多个异常类：@Transactional(noRollbackFor={RuntimeException.class, Exception.class})

# Springboot下的springMVC

Spring Boot下的Spring MVC和之前的Spring MVC使用是完全一样的，这里主要介绍spring支持的处理器注解

* `@Controller`基本的处理器注解

* `@RestController`

    是@Controller与@ResponseBody的组合注解
    	如果一个Controller类添加了@RestController，那么该Controller类下的所有方法都相当于添加了@ResponseBody注解

* `RequestMapping`设置资源路径支持Get请求，也支持Post请求

* `@GetMapping`

    RequestMapping和Get请求方法的组合
    只支持Get请求
    Get请求主要用于查询操作

    下面的注解类似

* `@PostMapping`Post请求主要用户新增数据

* `@PutMapping`Put通常用于修改数据

* `@DeleteMapping`通常用于删除数据



# Springboot实现RESTful

一种互联网软件架构设计的风格，提出了一组客户端和服务器交互时的架构理念和设计原则：

访问资源：请求资源，然后按照请求的方式进行处理，如果说get方式，查询操作，如果put 更新操作，如果是delete方式 删除资源，如果是post方式 添加资源

## 实现

Springboot为rest风格的编程提供了一下注解：

* `@PathVariable`获取url中的路径变量

使用之前介绍的`@PostMapping,@GetMapping,@DeleteMapping,@PutMapping`

并在路径中设置路径变量,通过中括号：

`@PostMapping("/springBoot/student/{name}/{age}")`

案例：

~~~java
@PostMapping(value = "/springBoot/student/{name}/{age}")
public Object addStudent(@PathVariable("name") String name,
                             @PathVariable("age") Integer age) {
        Map<String,Object> retMap = new HashMap<String, Object>();
        retMap.put("name",name);
        retMap.put("age",age);
        return retMap;
    }
~~~

## RESTful原则

* 增post请求、删delete请求、改put请求、查get请求
* 请求路径不要出现动词
* 分页、排序等操作，不需要使用斜杠传参数

# Springboot集成Redis

## 依赖

~~~xml
<!-- 加载spring boot redis包 -->
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
~~~

## 配置

~~~yaml
spring:
	redis:
		host: 192.168.92.134
		port: 6379
		password: 123456
~~~

## RedisTemplate

springboot提供了RedisTemplate类，针对redis的操作进行了薄层封装

### 键

RedisTemplate针对redis的key操作进行封装：

* `void rename(K oldKey, K newKey)`

    修改 redis 中 key 的名称

* `Boolean renameIfAbsent(K oldKey, K newKey)`

    如果旧值 key 存在时，将旧值改为新值

* `Boolean hasKey(K key)`

    判断是否有 key 所对应的值，有则返回 true，没有则返回 false

* `Boolean delete(K key)`

    删除指定的key

* `Long delete(Collection<K> keys)`

    批量删除 key

* `Boolean expire(K key, long timeout, TimeUnit unit)`
    设置过期时间

* `Boolean expireAt(K key, Date date)`

    设置过期时间

* `Long getExpire(K key)`

    返回当前 key 所对应的剩余过期时间

* `Long getExpire(K key, TimeUnit timeUnit)`

    返回剩余过期时间并且指定时间单位

* `Set<K>	keys(K pattern)`

    查找匹配的 key 值，返回一个 Set 集合类型

* `Boolean persist(K key)`

    将 key 持久化保存

* `Boolean move(K key, int dbIndex)`

    将当前数据库的 key 移动到指定 redis 中数据库当中

### 值

RedisTemplate针对redis值的五种数据类型，提供不同的封装类：

非绑定key操作：

* `ValueOperations<K, V> opsForValue()`
* `<HK, HV> HashOperations<K, HK, HV> opsForHash()`
* `ListOperations<K, V> opsForList()`
* `SetOperations<K, V> opsForSet()`
* `ZSetOperations<K, V> opsForZSet()`

绑定key操作：

* `BoundValueOperations<K, V> boundValueOps(K key)`
* `<HK, HV> BoundHashOperations<K, HK, HV> boundHashOps(K key)`
* `BoundListOperations<K, V> boundListOps(K key)`
* `BoundSetOperations<K, V> boundSetOps(K key)`
* `BoundZSetOperations<K, V> boundZSetOps(K key)`

Operations的方法与Jedis类似

## redis作为数据库缓存

### 设计思路

* 接受到查询数据的请求
* 首先访问redis查询
    * 查询到数据，缓存命中，返回数据
    * 没有查询到数据
        * 查询数据库，将结果存入redis，并返回给用户

### 代码实现

```java
public Long queryAllStudentCount() {
    //设置redisTemplate对象key的序列化方式
    redisTemplate.setKeySerializer(new StringRedisSerializer());
    //从redis缓存中获取总人数
    Long allStudentCount = (Long) redisTemplate.opsForValue().get("allStudentCount");
    //判断是否为空
    if (null == allStudentCount) {
        //去数据库查询，并存放到redis缓存中
        System.out.println("数据库查询");
        allStudentCount = studentMapper.selectAllStudentCount();
        redisTemplate.opsForValue().set("allStudentCount",allStudentCount,30, TimeUnit.SECONDS);
    }else{
        System.out.println("缓存命中");
    }
    return allStudentCount;
}
```

### 缓存穿透

上面的代码在并发环境下会出现缓存穿透，缓存中已经有数据，但请求仍然会访问数据库

需要改进代码，进行同步，进行两次次请求两次判断

~~~java
public Long queryAllStudentCount() {
    //设置redisTemplate对象key的序列化方式
    redisTemplate.setKeySerializer(new StringRedisSerializer());
    //从redis缓存中获取总人数
    Long allStudentCount = (Long) redisTemplate.opsForValue().get("allStudentCount");
    if(null == allStudentCount){
        synchronized (this){
            allStudentCount = (Long) redisTemplate.opsForValue().get("allStudentCount");
            //判断是否为空
            if (null == allStudentCount) {
                //去数据库查询，并存放到redis缓存中
                System.out.println("-----数据库查询------");
                allStudentCount = studentMapper.selectAllStudentCount();
                redisTemplate.opsForValue().set("allStudentCount",allStudentCount,30, TimeUnit.SECONDS);
            }else{
                System.out.println("------缓存命中-------");
            }
        }
    }else{
        System.out.println("------缓存命中-------");
    }
    return allStudentCount;
}
~~~



# Springboot继承Dubbo

## 依赖

~~~xml
<!--Spring Boot集成Dubbo的起步依赖-->
<dependency>
   <groupId>com.alibaba.spring.boot</groupId>
   <artifactId>dubbo-spring-boot-starter</artifactId>
   <version>2.0.0</version>
</dependency>
<!--ZooKeeper注册中心依赖-->
<dependency>
   <groupId>com.101tec</groupId>
   <artifactId>zkclient</artifactId>
   <version>0.10</version>
</dependency>
~~~

## 配置

~~~yaml

spring:
	application:
		#配置Dubbo应用名称，必须有且唯一
		name:
	dubbo:
		#配置是服务提供者，可省略
		server: 
		#配置注册中心地址
		registry: zookeeper://192.168.92.134:2181
~~~

## 注解

* 开启Dubbo支持

~~~java
@SpringBootApplication
@EnableDubboConfiguration//开启Dubbo配置支持
public class Application {
   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }
}

~~~

* 服务提供者

~~~java
mport com.alibaba.dubbo.config.annotation.Service;
import org.springframework.stereotype.Component;
//@Service是由阿里提供的注解，不是spring的注册
//@Service相当于 <dubbo:service interface="" ref="" version="" timeout=""/>
//如果提供者指定version,那么消费者也得指定version
@Service(interfaceClass = UserService.class,version = "1.0.0",timeout = 15000)
@Component  //将接口实现类交给spring容器进行管理
public class UserServiceImpl implements UserService {
    @Override
    public String say(String name) {
        return "Hello SpringBoot!";
    }
}
~~~

* 服务消费者

~~~java
@RestController
public class UserController {
    //@Reference注解 相当于<dubbo:reference id="" interface="" version="" check="false"/>
    //通过远程调用注入服务提供者
    @Reference(interfaceClass = UserService.class,version = "1.0.0",timeout = 15000,check=false)
    private UserService userService;

    @RequestMapping(value = "/springBoot/hello")
    public Object hello(HttpServletRequest request) {
        String sayHello = userService.say("SpringBoot");
        return sayHello;
    }
}
~~~

