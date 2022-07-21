# maven

核心功能

* 项目构建
* 依赖管理

# 配置maven

通过settings.xml文件来配置maven

* `localRepository`本地仓库路径
* `pluginGroups`插件
* `mirrors`镜像
* `profile`JDK版本

# Maven工程项目结构

* src

    * main
        * java 
        * resources
        * [webapp] web应用目录，在web项目下生成

    * test
        * java
        * resources

* target

* pom.xml

# 依赖管理

通过pom.xml中的dependencies标签进行依赖管理

~~~xml
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.2</version>
</dependency>
~~~

# 资源配置扫码

~~~xml
<build>
<!--配置资源扫描-->
  <resources>
    <resource>
      <directory>src/main/java</directory><!--所在的目录-->
      <includes><!--包括目录下的.properties,.xml 文件都会扫描到-->
        <include>**/*.properties</include>
        <include>**/*.xml</include>
      </includes>
      <!-- filtering 选项 false 不启用过滤器， *.property 已经起到过滤的作用了 -->
      <filtering>false</filtering>
    </resource>
  </resources>
</build>
~~~

# 多模块管理

如果一个项目中有多个模块，那么模块之间的依赖和插件可能会有版本冲突

maven通过继承的思想解决了多模块下版本冲突的问题

一个项目中如果有父子关系模块，那么这个项目被称为聚合项目

* 父模块：负责管理其子模块的依赖和插件，没有代码内容

    定义一个父模块，需要：

    1. 更改打包方式为pom：`<packaging>pom</packaging>`
    2. 删除src文件夹，以防止可能的项目结构冲突

* 子模块：通过定义`<parent>`标签指定自己的父母（通过父模块的GAV坐标）：

    ~~~xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.1</version>
        <relativePath/>
    </parent>
    ~~~

## 聚合项目的依赖管理

在聚合项目中，可能并不是所有的项目都需要父模块的依赖，maven提供了management标签来管理

对于父模块

* `<dependencies>`标签下的依赖都会被子模块继承

* `<dependencyManagement>`标签下的依赖不会直接被子模块继承

    当子模块需要时，可以显式地声明父模块该标签下的依赖以继承需要的依赖

    子模块声明时，不需要再声明依赖的版本，会自动继承父模块的版本

    子模块声明示例：

    ~~~xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    ~~~

    

## 通过properties标签管理依赖版本

在properties标签下可以自定义属性：标签名为属性名，标签值为属性值

通过`${属性名}`的方式调用

示例：

~~~xml
<!--定义属性 -->
<properties>
    <lombok.version>1.18.2</lombok.version>
</properties>

<!--调用属性 -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>${lombok.version}</version>
</dependency>
~~~









