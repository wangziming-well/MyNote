# 配置maven

~~~xml
<!--mybatis-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.3</version>
</dependency>
<!-- mysql-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.19</version>
</dependency>

<!--spring框架核心依赖 beans core context-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>


<!--spring: 实现aop依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
<!--spring整合mybatis-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.3</version>
</dependency>
<!--spring管理事务-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>

<!--springMVC核心依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.3.RELEASE</version>
</dependency>
<!--tomcat： servlet jsp el jstl standard-->
<dependency>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>tomcat-servlet-api</artifactId>
    <version>9.0.19</version>
</dependency>
<dependency>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>tomcat-jsp-api</artifactId>
    <version>7.0.47</version>
</dependency>
<dependency>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>tomcat-el-api</artifactId>
    <version>7.0.47</version>
</dependency>

<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
<dependency>
    <groupId>org.apache.taglibs</groupId>
    <artifactId>taglibs-standard-jstlel</artifactId>
    <version>1.2.5</version>
</dependency>
<!--文件上传-->
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.1</version>
</dependency>

<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.9.0</version>
</dependency>
<!--json: jackson-->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.0</version>
</dependency>
</dependencies>
<!--配置资源扫描-->
<resources>
    <resource>
        <directory>src/main/java</directory>
        <includes>
            <include>**/*.xml</include>
            <include>**/*.properties</include>
        </includes>
    </resource>
    <resource>
        <directory>src/main/resources</directory>
        <includes>
            <include>**/*.*</include>
        </includes>
    </resource>
</resources>
~~~

# 配置mybatis.xml

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--1.配置读取属性文件prop.properties-->
    <!--2.配置全局设置settings-->
    <settings>
        <!--打印日志-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
    <!--3.配置环境数据源  交由spring管理-->
    <!--4.配置mapper映射 交由spring管理-->
</configuration>
~~~



# 配置spring.xml

## spring管理mybatis

* 管理DataSource
* 管理mapperScan
* 管理sqlSessionFactory

~~~xml
<!--管理mybatis-->
<!--1.读取数据库配置文件，如果有的话-->
<!--<context:property-placeholder location="classpath:"/>-->
<!--2.管理DataSource-->
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <!--配置数据源-->
    <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/empproject?serverTimezone=UTC"/>
    <property name="username" value="root"/>
    <property name="password" value="root"/>
</bean>
<!--3.管理SqlSessionFactory
        sqlSessionFactory必须读取数据源和mybatis.xml 来生成sqlSession
    -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="configLocation" value="classpath:mybatis.xml"/>
</bean>
<!--4.管理mapper
        spring会根据sqlSessionFactory管理mapperScanner对象
        mapperScanner会
        根据SqlSessionFactory生成的sqlSession，扫描mapper接口与mapper.xml，根据动态代理
        生成mapper接口的实现类 并直接被spring管理-->
<bean id="mapperScan" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <!--mapper扫描器会扫描并管理指定包下的所有mapper配置文件与接口-->
    <property name="basePackage" value="com.bjpn.mapper"/>
    <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
</bean>
~~~

## spring管理事务

* 配置事务管理器
* 配置事务通知器
* 配置aop

~~~xml
<!--配置事务管理-->
<!--1.配置事务管理器-->
<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--读取数据源-->
    <property name="dataSource" ref="dataSource"/>
</bean>
<!--2.配置事务管理器的通知器，配置事务传播行为-->
<tx:advice id="txAdvice" transaction-manager="txManager">
    <tx:attributes>
        <!-- 传播行为 -->
        <!--明确你的增删改的方法名-->
        <tx:method name="save*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="insert*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="add*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="delete*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="update*" propagation="REQUIRED" rollback-for="Exception"/>
        <!--查询可以不要事务-->
        <tx:method name="find*" propagation="SUPPORTS" read-only="true" />
        <tx:method name="get*" propagation="SUPPORTS" read-only="true" />
        <tx:method name="loginUserService" propagation="SUPPORTS" read-only="true" />
    </tx:attributes>
</tx:advice>
<!--3.配置事务aop-->
<aop:config>
    <!--配置切点，所有的service方法都需要事务-->
    <aop:pointcut id="allServiceMethod" expression="execution(* com.bjpn.service..*.*(..))"/>
    <!--配置通知器-->
    <aop:advisor advice-ref="txAdvice" pointcut-ref="allServiceMethod"/>
</aop:config>
~~~



## spring配置springmvc

* 加载处理器映射器，出其里适配器
* 扫描controller
* 处理静态资源
* 配置视图解析器
* 配置文件上传解析器
* 配置拦截器

~~~xml
<!--配置springMVC-->
<!--1.加载处理器映射器，处理器适配器-->
<mvc:annotation-driven/>
<!--2.扫描controller-->
<context:component-scan base-package="com.bjpn.controller"/>
<!--3.处理静态资源-->
<mvc:default-servlet-handler/>
<!--4.配置视图解析器-->
<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/"/>
    <property name="suffix" value=".jsp"/>
</bean>
<!--5.配置文件上传解析器-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <property name="maxUploadSize" value="#{1024*1024*80}"/>
</bean>
<!--TODO 6.配置拦截器-->
~~~



## spring配置ioc与aop

* 管理指定包下的类
* 管理aop

~~~xml
<!--配置spring ioc和aop-->
<!--1.配置ioc-->
<context:component-scan base-package="com.bjpn.bean;com.bjpn.service;com.bjpn.dao"/>
<!--TODO 2.配置aop-->
~~~





# 配置web.xml文件

* 头文件约束版本需要3.0以上
* 用监听器加载spring
* 配置中央控制器
* 配置字符过滤器

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--配置spring容器-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <!--springMVC中央控制器-->
    <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!--配置字符过滤器-->
    <filter>
        <filter-name>charEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>charEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
~~~





























