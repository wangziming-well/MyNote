# 配置maven

~~~xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.bjpn</groupId>
  <artifactId>crmproject</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>crmproject Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>
    <!--搭建ssm环境-->
    <!--mybatis
      mybatis   mysql驱动    数据库连接池的包：c3p0   dbcp  druid
    -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.3</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.19</version>
    </dependency>
    <!--数据库连接池的依赖-->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.1</version>
    </dependency>
    <!--spring
      spring管理mybatis
      spring的核心  core  beans  context  aop
         切面框架
         jdbc  tx
    -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.3</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <!--aop-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <!--jdbc和事务-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <!--springMVC
       servlet  jsp  el  jstl  standard
       spring-web  spring-webmvc
       jackson-core   databind   annotations
       fileupload  io
    -->
    <dependency>
      <groupId>org.apache.tomcat</groupId>
      <artifactId>tomcat-jsp-api</artifactId>
      <version>7.0.47</version>
    </dependency>
    <dependency>
      <groupId>org.apache.tomcat</groupId>
      <artifactId>tomcat-servlet-api</artifactId>
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
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
    </dependency>
    <!-- spring-web  spring-webmvc-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.3.RELEASE</version>
    </dependency>
    <!--jackson-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.13.1</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.13.1</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-annotations</artifactId>
      <version>2.13.1</version>
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
  </dependencies>

  <build>
    <!--读取资源文件-->
    <resources>
      <!--配置资源扫描的-->
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
    <finalName>crmproject</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

~~~





# 配置mybatis

Applicationcontext-datasource.xml

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
   http://www.springframework.org/schema/context
   http://www.springframework.org/schema/context/spring-context-4.0.xsd
   http://www.springframework.org/schema/aop
   http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
  http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
    <!--spirng整合mybatis-->
    <!--1、数据源datasource
        使用druid数据库连接池
    -->
    <bean id="myDataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <!--配置连接参数
            druid可以不写驱动类  他会自动扫描你的驱动jar包  根据不同版本的驱动包  自动引入不同的驱动类
        -->
        <!--<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>--><!--可以让他自动生成-->
        <property name="url" value="jdbc:mysql://localhost:3306/crm2203?serverTimezone=UTC"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>
    <!--2、sqlSessionFactory-->
    <bean id="mySqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="myDataSource"/>
        <!--如果你有mybatis.xml  可以在这里引入-->
        <property name="configLocation" value="classpath:mybatis.xml"/>
    </bean>
    <!--3、mapper扫描器-->
    <!--spring会根据mySqlSessionFactory  管理mapperScanner对象
        mapperScanner会
        根据SqlSessionFactory生成的sqlSession ，扫描mapper接口和mapper.xml，根据动态代理
        生成该mapper接口的实现类  直接被spring管理
    -->
    <bean id="mapperScan" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--mapper扫描器会扫描  这个包下所有的 mapper接口和mapper.xml-->
        <property name="basePackage" value="com.bjpn.settings.mapper;com.bjpn.workbench.mapper"/>
        <!--sqlSessionFactory可以生成sqlSession
            根据扫描到的mapper接口和mapper.xml文件自动生成  mapper的实现类
            mapper接口和mapper.xml文件的名字一致
        -->
        <property name="sqlSessionFactoryBeanName" value="mySqlSessionFactory"/>
    </bean>
    <!--把spring的事务传播行为写在数据库位置-->
    <!--spring根据aop管理了事务-->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="myDataSource"/>
    </bean>
    <!--设置切点和通知器-->
    <aop:config>
        <aop:pointcut id="allServiceMethod" expression="execution(* com.bjpn..service.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="allServiceMethod"/>
    </aop:config>
    <!--配置通知器  spring的事务传播行为-->
    <tx:advice id="txAdvice" transaction-manager="txManager">
        <tx:attributes>
            <!-- 传播行为 -->
            <!--明确你的增删改的方法名-->
            <tx:method name="save*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="insert*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="add*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="jia*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="delete*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="remove*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="update*" propagation="REQUIRED" rollback-for="Exception"/>
            <tx:method name="edit*" propagation="REQUIRED" rollback-for="Exception"/>
            <!--查询可以不要事务-->
            <tx:method name="find*" propagation="SUPPORTS" read-only="true" />
            <tx:method name="get*" propagation="SUPPORTS" read-only="true" />
            <tx:method name="loginUserService" propagation="SUPPORTS" read-only="true" />
        </tx:attributes>
    </tx:advice>
</beans>

~~~



# 配置spring

Applicaitoncontext.xml

~~~xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
   http://www.springframework.org/schema/context
   http://www.springframework.org/schema/context/spring-context-4.0.xsd">
    <!--spring的核心配置-->
    <!--把类扫描到spring容器中-->
    <context:component-scan base-package="com.bjpn.settings.bean;com.bjpn.settings.service;
                                           com.bjpn.workbench.bean;com.bjpn.workbench.service"/>
    <!--数据源需要被spring容器管理  服务器启动的时候就要加载了-->
    <!--让spring管理datasource-->
    <import resource="classpath:applicationcontext-datasource.xml"/>
</beans>

~~~

# 配置springmvc

Applicationcontext-mvc.xml

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"

       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
   http://www.springframework.org/schema/context
   http://www.springframework.org/schema/context/spring-context-4.0.xsd
   http://www.springframework.org/schema/mvc
  http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd">
    <!--1、加载处理器映射器  适配器-->
    <mvc:annotation-driven/>
    <!--2、扫描controller-->
    <context:component-scan base-package="com.bjpn.settings.controller;com.bjpn.workbench.controller"/>
    <!--3,静态资源处理-->
    <mvc:default-servlet-handler/>
    <!--4、视图解析器 -->
    <bean id="myViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/pages/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    <!--5、文件上传解析器    multipartResolver这个名字不能改变-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="maxUploadSize" value="#{1024*1024*80}"/>
        <!--<property name="defaultEncoding" value="utf-8"/>-->
    </bean>
    <!--6、拦截器-->
</beans>

~~~



# 配置web

web.xml

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
 <!--1、监听器启动spring容器-->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationcontext.xml</param-value>
  </context-param>
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <!--2、配置中央控制器-->
  <servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:applicationcotext-mvc.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  <!--3、post乱码问题-->
  <filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
</web-app>
~~~

