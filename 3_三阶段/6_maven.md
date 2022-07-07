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

## 资源配置扫码

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

