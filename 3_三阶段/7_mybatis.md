# mybatis介绍

* 是一个轻量级的提供半自动化SQL语句的持久层框架，封装了jdbc

* 核心思想是orm(对象关系映射)

* maven依赖

    ~~~xml
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.1</version>
    </dependency>
    ~~~

# 核心配置文件

## 配置文件约束

~~~xml
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
~~~

## 标签层级

- configuration（配置跟标签）
    - properties（属性）
    - settings（设置）
    - typeAliases（类型别名）
    - typeHandlers（类型处理器）
    - objectFactory（对象工厂）
    - plugins（插件）
    - environments（环境配置）
        - environment（环境变量）
            - transactionManager（事务管理器）
            - dataSource（数据源）
    - databaseIdProvider（数据库厂商标识）
    - mappers（映射器）

## properties

通过读取外部properties文件，或者内部设置，来配置属性

标签层级：

* properties [resource 指定外部properites位置]
    * property [name 属性名 ； value 属性值]

调用属性：

通过`${属性名}`动态替换配置属性

示例：

~~~xml
<properties resource="org/mybatis/example/config.properties">
  <property name="username" value="dev_user"/>
  <property name="password" value="F2Fa3!33TYyg"/>
</properties>

<!-- 使用属性 -->

<dataSource type="POOLED">
  <property name="driver" value="${driver}"/>
  <property name="url" value="${url}"/>
  <property name="username" value="${username}"/>
  <property name="password" value="${password}"/>
</dataSource>
~~~

## settings

是mybatis的全局设置，会改变MyBatis的运行时行为

标签层级

* settings
    * setting [name ，value] 

示例：

~~~xml
<!--常用设置：开启日志输出-->
<settings>
    <setting name="logImpl" value="STDOUT_LO" />
</settings>
~~~

## typeAliases

类型别名可为Java类型设置别名

标签层级：

* typeAiases

    * typeAlias [alias:别名 ，type:java类全限定名]

    * package[name:包名]

        在指定包名中的每一个类，在没有注解的情况下，mybatis将使用类的首字母小写的非限定名来作为它的别名，若有注解，则别名为注解值：

示例：

~~~xml
<tpyeAliases>
	<typeAlias alias="author" type="com.bean.Author" />
	<package name = "com.bean"/>
</tpyeAliases>
~~~

同时mybatis内置了一些常用的类别名：

| 别名                      | 映射的类型   |
| :------------------------ | :----------- |
| _byte                     | byte         |
| _char (since 3.5.10)      | char         |
| _character (since 3.5.10) | char         |
| _long                     | long         |
| _short                    | short        |
| _int                      | int          |
| _integer                  | int          |
| _double                   | double       |
| _float                    | float        |
| _boolean                  | boolean      |
| string                    | String       |
| byte                      | Byte         |
| char (since 3.5.10)       | Character    |
| character (since 3.5.10)  | Character    |
| long                      | Long         |
| short                     | Short        |
| int                       | Integer      |
| integer                   | Integer      |
| double                    | Double       |
| float                     | Float        |
| boolean                   | Boolean      |
| date                      | Date         |
| decimal                   | BigDecimal   |
| bigdecimal                | BigDecimal   |
| biginteger                | BigInteger   |
| object                    | Object       |
| date[]                    | Date[]       |
| decimal[]                 | BigDecimal[] |
| bigdecimal[]              | BigDecimal[] |
| biginteger[]              | BigInteger[] |
| object[]                  | Object[]     |
| map                       | Map          |
| hashmap                   | HashMap      |
| list                      | List         |
| arraylist                 | ArrayList    |
| collection                | Collection   |
| iterator                  | Iterator     |

## environments

可以配置多种环境来应用与多种数据库

标签层级

* environments [default: 默认环境]
    * environment [id:环境唯一标识]
        * transactionManager [type 事务管理类型]
        * dataSource [type 数据源类型]
            * property [name,value]

示例:

~~~xml
<environments default="development">
  <environment id="development">
    <transactionManager type="JDBC">
      <property name="..." value="..."/>
    </transactionManager>
    <dataSource type="POOLED">
      <!--必须指定driver,url,username,password)以连接数据源 -->
      <property name="driver" value="${driver}"/>
      <property name="url" value="${url}"/>
      <property name="username" value="${username}"/>
      <property name="password" value="${password}"/>
    </dataSource>
  </environment>
</environments>
~~~

## mappers

用以定义SQL映射语句

层级关系

* mappers
    * mapper[resource:指定mapper配置文件的路径 class:使用映射器接口实现类的完全限定类名]
    * package[name:将包内的映射器接口实现全部注册为映射器]

示例：

~~~xml
<mappers>
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <mapper resource="org/mybatis/builder/BlogMapper.xml"/>
  <mapper resource="org/mybatis/builder/PostMapper.xml"/>
</mappers>
~~~



# mapper映射配置文件

## 配置文件约束

~~~xml
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
~~~

## 标签层级

* mapper[username :mapper配置文件的唯一标识]
    * select
    * insert
    * update
    * delete
    * sql
    * resultMap

## select

定义查询语句

属性：

* id:在命名空间中的位移标识符，可以被用来引用这条语句
* parameterType:将会传入这条语句的参数的类全限定名或者别名
* resultType:期望从这条语句中返回结果的类全限定名或别名
* resultMap:对外部resultMap的命名引用

resultTpye与resultMap只能使用一个

示例：

~~~xml
<select id="selectPerson" parameterType="int" resultTpye="hashmap">
    select * from person where ID=#{id}
</select>
~~~



## insert、update、delete

分别定义了插入、更新、删除语句

它们都具有属性：

* id:在命名空间中的位移标识符，可以被用来引用这条语句
* parameterTpye:将会传入这条语句的参数的类全限定名或者别名



## sql

定义用来可复用的SQL代码片段，以在其他语句中使用

属性：

* id 调用时的唯一标识符

调用：

在sql语句中用\<include>标签调用，用\<property>指定sql中动态参数

示例：

~~~xml
<!--定义 -->
<sql id="userColumns">
	id,name,${s}
</sql>

<!--调用 -->
<select id="selectUsers">
	select 
    <include refid="userColumns">
        <property name="s" value="sex" />
    </include>
    from
    user
</select>
~~~

该标签输出的sql语句为:

~~~sql
select id,name,sex from user
~~~



## 参数传递

在mybatis的mapper配置文件的sql语句中，用`#{}`和`${}`接受java传递的参数

* `#{}`代表占位符，使用preparedStatement对象，当只传递一个参数时，参数名可以是任意的
* `${}`代表拼接，使用statement

参数名由ParameterType决定，如果是类，则参数名为类属性，如果是map则参数名为map的键名



## resultMap

当指定的resultTpye中的属性或者键名与数据库的字段名一致时，mybatis会自动建立resultMap映射，将字段与属性或者键名建立映射关系，以传值并返回结果

当数据库的字段名与类的属性名不一致时，我们有两种解决方案

1. 在sql语句中为字段起别名
2. 手动建立关系映射resultMap，将resultType替换为配置好的resultMap

标签层级:

* resultMap[id,type]

    id：当前命名空间的唯一标识，用于标识一个结果映射

    type：类的全限定名，或者别名，表示关系映射所映射的类

    * id[property,column] 表示映射的为主键

    * result[property,column] 表示映射的是普通字段

        property：类的属性名

        column：数据库字段名

示例：

~~~xml
<!--定义关系映射 -->
<resultMap id="userResultMap" type="user">
	<id property="uid" column="user_id"/>
    <result property="uname" column="user_name"/>
    <result property="usex" column="user_sex"/>
</resultMap>

<!--调用关系映射 -->
<select resultMap="userResultMap">
	select user_id,user_name,user_sex from user
</select>
~~~



# 动态SQL

动态SQL提供了动态拼接SQL语句的功能

## if

属性：

* test：条件，条件为真，则拼接if中的SQL语句，否则不拼接

示例：

~~~xml
<select id="findUser" resultType="user">
	select * from user
    where sex="male"
    <if test="likeName !=null and likeName !=''">
    	and name like #{likeName}
    </if>
</select>
~~~

## where

当有多个where条件时，使用if语句可能会导致最终的SQL语句多出and关键字

所以mybatis设置了where标签，它：

* 自动拼装where关键字
* 自动去掉第一个条件的and

示例：

~~~xml
<select id="findUser" resultType="user">
	select * from user
    <where>
        <if test="sex !=null and sex !=''">
    		and sex="male"
        </if>
        <if test="likeName !=null and likeName !=''">
            and name like #{likeName}
        </if>
        <if test=test="age !=null and age !=''">
            and age =10
        </if>
    </where>
</select>
~~~

## set

执行修改语句时，当设有多个set字段时，使用if语句可能会导致最终SQL语句多出`,`

所以mybatis设置了set标签，它：

* 自动拼装set关键字
* 自动去掉最后一个参数的`,`

示例：

~~~xml
<update id="updateUser">
  update user
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
    </set>
  where id=#{id}
</update>
~~~



## trim

能指定sql语句的前后缀并去掉指定的sql关键字或字符

属性：

* prefix：给sql语句拼装的前缀
* suffix：给sql语句拼装的后缀
* prefixOverrides：如果sql语句前面是prefixOverrides指定的字符，则去掉该字符
* suffixOverrids：如果sql语句后面是prefixOverrides指定的字符，则去掉该字符

示例:

~~~xml
<insert id="insert" parameterType="account">
        insert into account
        <trim prefix="(" suffix=")" suffixOverrides=",">
            <if test="money != null">
                money,
            </if>
            <if test="name != null and name != ''">
                name
            </if>
        </trim>
        <trim prefix="values(" suffix=")" suffixOverrides=",">
            <if test="money != null">
               #{money},
            </if>
            <if test="name != null and name != ''">
                #{name}
            </if>
        </trim>
</insert>
~~~



## forEach

能遍历指定的集合，在in关键字中有应用

属性：

* open ：指定开始的字符
* separator：指定分隔符
* close：指定结束字符
* collection：指定要遍历的集合类型
* item：指定遍历的元素名
* index：指定遍历下标的变量名

示例：

~~~xml
<delete id="deleteBatch">
    delete from account where aid in
    <foreach collection="array" item="aid" open="(" close=")" separator=",">
        #{aid}
    </foreach>
</delete>
~~~

# SqlSession

SqlSession是使用Mybatis的主要Java接口，通过这个接口，我们可以:

* 执行命令
* 获取映射器示例和事务管理



## 获取SQLSession实例

* 通过(org.apache.ibatis.io)Resources工具类中的以下方法加载配置文件：

    InputStream getResourceAsStream(String resource)

* 通过SqlSessionFactoryBuilder类中的以下方法创建SqlSessionFactory实例：

    SqlSessionFactory build(InputStream inputStream)

* 通过SqlSessionFactory类中的以下方法创建SqlSession实例：

    SqlSession openSession()

注意：SqlSessionFactory是懒汉式单例模式

实例：

~~~java
//一个获得SqlSession的方法
public SqlSession getSqlSession(){
    if(sqlSessionFactory == null){
        try {
            InputStream in = Resources.getResourceAsStream("mybatis.xml");
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(in);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    SqlSession sqlSession = sqlSessionFactory.openSession();
    return sqlSession;
}
~~~



## 语句执行方法

* \<T> T selectOne(String statement, Object parameter)

    执行单条查询

* \<E> List\<E> selectList(String statement, Object parameter)

    执行多条查询

* int insert(String statement, Object parameter)

    执行插入语句

* int update(String statement, Object parameter)

    执行更新语句

* int delete(String statement, Object parameter)

    执行删除语句

statement参数定位到具体的语句，格式为`"mapperUsername.语句id"`

parameter为传给语句的参数

## 事务控制方法

* void commit()
    事务提交
* void rollback()
    事务回滚

## 关闭SqlSession

* void close()

    关闭

## 使用映射器

* \<T> T getMapper(Class\<T> type)

采用接口，使用代理的方式创建接口的实现类

type为mapper接口的Class文件

映射器接口需要满足：

* mapper映射文件名与mapper接口名

* namespace为mapper接口的全路径名
* sql标签中的id与mapper接口中对应方法名一致
* sql标签中的parameterType和mapper接口中的对应方法参数类型一致
* sql标签中的resultType和mapper接口中对应方法的返回值类型一致

**注意：**

* 如果映射方法需要接受多个参数，可以在参数前使用`@Param`注解来定义每个参数的名字

* 增删改的方法返回值除了int也可以是boolean类型，mybatis会自动转换
