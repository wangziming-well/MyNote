# 逆向工具依赖

在build标签下设置插件：

~~~xml
<plugins>
    <!--myBatis逆向工程插件-->
    <plugin>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-maven-plugin</artifactId>
        <version>1.3.2</version>
        <configuration>
            <verbose>true</verbose>
            <overwrite>true</overwrite>
        </configuration>
    </plugin>
</plugins>
~~~

# 核心配置文件

文件名必须是：

generatorConfig.xml

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>

    <!--指定mysql数据库驱动-->
    <!--<classPathEntry location="E://repository-p2p//mysql//mysql-connector-java//5.1.43//mysql-connector-java-5.1.43.jar"/>-->

    <!--导入属性配置   配置信息中有链接数据库的参数-->
    <!--<properties resource="generator.properties"></properties>-->

    <!--指定特定数据库的jdbc驱动jar包的位置
        注意：驱动类需要找到他在本机的绝对位置   不能有空格和中文路径
    -->
    <!--TODO 需要修改-->
    <classPathEntry location="D:/Data/Learning/Java/repository/mysql/mysql-connector-java/8.0.15/mysql-connector-java-8.0.15.jar"/>

    <context id="default" targetRuntime="MyBatis3">

        <!-- optional，旨在创建class时，对注释进行控制，false生成注释,true无注释 -->
        <commentGenerator>
            <property name="suppressDate" value="true"/>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>

        <!--jdbc的数据库连接
            逆向工程会扫描你数据库中的指定表  你多个数据库可能会出现同名的表
            他会找第一个出现的表名
            nullCatalogMeansCurrent：无视其他同名表  只生成指定数据库中的表
            在url上配置参数
            jdbc:mysql://localhost:3306/sh2203?serverTimezone=UTC&nullCatalogMeansCurrent=true
         -->
        <!--TODO 需要修改-->
        <jdbcConnection
                driverClass="com.mysql.cj.jdbc.Driver"
                connectionURL="jdbc:mysql://localhost:3306/empproject?serverTimezone=UTC"
                userId="root"
                password="root">
            <property name="nullCatalogMeansCurrent" value="true"/>
        </jdbcConnection>


        <!-- 非必需，类型处理器，在数据库类型和java类型之间的转换控制-->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>


        <!-- Model模型生成器,用来生成含有主键key的类，记录类 以及查询Example类
            targetPackage     指定生成的model生成所在的包名
            targetProject     指定在该项目下所在的路径|指定生成到的工程名称
            1、根据数据库的表生成对应的java实体类
            targetPackage：实体类所在位置
            targetProject:包的位置  必须是本地路径
        -->
        <!--TODO 需要修改-->
        <javaModelGenerator targetPackage="com.bjpn.bean"
                            targetProject="D:/Data/Learning/Java/workspace/ssm/src/main/java">

            <!-- 是否允许子包，即targetPackage.schemaName.tableName -->
            <property name="enableSubPackages" value="false"/>
            <!-- 是否对model添加 构造函数 true添加，false不添加
                不生成有参构造  否则mapper.xml文件的关系映射会使用有参构造  不利于我们操作
            -->
            <property name="constructorBased" value="false"/>
            <!-- 是否对类CHAR类型的列的数据进行trim操作 -->
            <property name="trimStrings" value="true"/>
            <!-- 建立的Model对象是否 不可改变  即生成的Model对象不会有 setter方法，只有构造方法 -->
            <property name="immutable" value="false"/>
        </javaModelGenerator>

        <!--Mapper映射文件生成所在的目录 为每一个数据库的表生成对应的SqlMap文件 -->
        <!--2、生成mapper.xml
            targetPackage：mapper.xml所在位置
            targetProject:包的位置  必须是本地路径   只用到src/main/java
        -->
        <!--TODO 需要修改-->
        <sqlMapGenerator targetPackage="com.bjpn.mapper"
                         targetProject="D:/Data/Learning/Java/workspace/ssm/src/main/java">
            <property name="enableSubPackages" value="false"/>
        </sqlMapGenerator>

        <!-- 客户端代码，生成易于使用的针对Model对象和XML配置文件 的代码
                type="ANNOTATEDMAPPER",生成Java Model 和基于注解的Mapper对象
                type="MIXEDMAPPER",生成基于注解的Java Model 和相应的Mapper对象
                type="XMLMAPPER",生成SQLMap XML文件和独立的Mapper接口
        -->
        <!--3、生成mapper接口的位置
            targetPackage：mapper.xml所在位置
            targetProject:包的位置  必须是本地路径   只用到src/main/java
            mapper接口和mapper.xml文件的路径要求一致
        -->
        <!--TODO 需要修改-->
        <javaClientGenerator targetPackage="com.bjpn.mapper"
                             targetProject="D:/Data/Learning/Java/workspace/ssm/src/main/java" type="XMLMAPPER">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!--4、根据指定的表  生成对应的信息
            tableName：表名
            domainObjectName：根据这个表生成的实体类的名字
            enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false"
               不会产生一个额外的Example类
               只会产生基本增删改查方法
        -->
        <!--TODO 需要修改-->
        <table tableName="emp" domainObjectName="Employee"
               enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>
        <table tableName="dept" domainObjectName="Department"
               enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>
        <table tableName="admin" domainObjectName="Administrator"
               enableCountByExample="false" enableUpdateByExample="false"
               enableDeleteByExample="false" enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>
    </context>
</generatorConfiguration>
~~~

