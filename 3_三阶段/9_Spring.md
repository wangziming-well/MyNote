# Spring简介

Spring是一个轻量级的Java开发框架，核心是：

* 控制反转(IOC)
* 面向切面编程(AOP)

是一个容器管理对象

集成整合了各种优秀框架

# Spring环境搭建

maven依赖：

~~~xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
~~~

核心配置文件的头约束：

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans-4.1.xsd">
    <!--beans  就是对象容器-->
</beans>
~~~

# IOC控制反转

控制反转(Inversion of Control)指将由程序代码直接操控的对象调用权交给容器，通过容器来实现对象的装配与管理



## 简单的IOC实现

通过配置文件配置要被string容器管理的类：

* 默认调用无参构造创建对象

如果没有指定id，则id为类名的驼峰式命名；

~~~xml
<!--配置要被容器管理的类 id：唯一标识 class类的全限定名 -->
<bean id="u" class="com.bjpn.bean.User"/>
~~~

* 调用有参构造创建对象

~~~xml
<bean id="u1" class="com.bjpn.bean.User">
    <constructor-arg name="password" value="123"/>
    <constructor-arg name="username" value="123"/>
</bean>
~~~

* 调用set方法：

    需要对象由无参构造

~~~xml
<bean id="u2" class="com.bjpn.bean.User">
    <property name="username" value="321"/>
    <property name="password" value="321"/>
</bean>
~~~



从Spring容器中获取对象：

~~~java
public void testIOC(){
    ClassPathXmlApplicationContext ioc = new ClassPathXmlApplicationContext("spring.xml");
    User user = (User)ioc.getBean("u");
    System.out.println(user);
}
~~~



## DI依赖注入：IOC高级用法

classA中含有classB的实例，则classA对classB有依赖

如果讲classA控制反转，交由spring容器管理，那么classA中的classB实例也应该交由spring容器创建

再传递给classA

所以想要实现依赖注入，classA，classB都需要交由spring容器管理；并且classA需要有classB类型的属性，以方便spring进行依赖注入：

~~~xml
<!--依赖类与被依赖类都需要被spring容器管理 -->
<bean id="userDao" class="com.bjpn.dao.UserDao" />
<bean id="userService" class="com.bjpn.service.UserService">
    <property name="userDao" ref="userDao"/>
</bean>
~~~



## 基于注解的IOC

配置注解扫描：

~~~xml
<!--扫描指定包下的所有注解-->
<context:component-scan base-package="com.bjpn"/>
~~~

实体类注解：

* `@controller`表示处理器类
* `@Service`当前类为业务层
* `@Respository`当前类为持久层
* `@Component`普通类

以上注解都有name属性，即配置中的id；不写默认是类名的驼峰式

依赖注入注解：

* `@Autowired`在属性上，表示该属性由容器根据set方法进行依赖注入
* `@Qualifier`辅助注解，指定要注入的类（在属性为接口，且项目中该接口不止有一个实现类时）



示例：

~~~java
//被依赖类
@Repository
public class UserDao {
    public void addUser(){
        System.out.println("我是dao方法");
    }
}
//依赖类
@Service
public class UserService {
    @Autowired
    @Qualifier("userDao")
    private UserDao userDao= null;

    public void register(){
        userDao.addUser();
    }
}
~~~



# AOP面向切面编程

在生产环境中，经常有业务交叉的情况；为了实现业务交叉时的解耦和，产生了面向切面的思想。

通过动态代理的方式，将增强类的功能插入到目标类中

## AOP术语

* 切面Aspect

    泛指交叉业务逻辑

* 连接点JoinPoint

    指被切面织入的具体方法

* 切入点Pointcut

    指声明的一个或多个连接点的集合

* 目标对象Target

    指要被增强的

* 通知Advice

    表示切面的执行时间

## AsperctJ实现AOP

Spring整合了Asperct框架以实现AOP

### maven依赖

~~~xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
~~~

### 通知类型

* 前置通知 `@Before`
* 后置通知`@After`
* 环绕通知`@Around`
* 异常通知`@AfterThrowing`
* 最终通知`@AfterReturning`

### 切入表达式

AspectJ 用切入表达式的形式指定切入点

表达式形式为:

`execution(modifiers-pattern? ret-type-pattern declariong-type-pattern? name-pattern(param-pattern) throws-pattern?)`

* `?`表示可选匹配
* `modifiers-pattern`匹配访问权限类型
* `ret-type-pattern`匹配返回值类型
* `declaring-type-pattern`匹配包名类名
* `name-pattern(param-pattern)`匹配方法名(参数)
* `throws-pattern`匹配异常

以上匹配可以由符号表示含义：

* `*`

    0至多个任意字符

* `..`

    * 在方法参数中，表示任意多个参数
    * 在包名后，表示当前包及其子包路径

* `+`

    * 在类名后，表示当前类及其子类
    * 在接口后，表示当前接口及其实现类

示例：

~~~
举例：
execution(public * *(..)) 
指定切入点为：任意公共方法。
execution(* set*(..)) 
指定切入点为：任何一个以“set”开始的方法。
execution(* com.xyz.service.*.*(..)) 
指定切入点为：定义在 service 包里的任意类的任意方法。
execution(* com.xyz.service..*.*(..))
指定切入点为：定义在 service 包或者子包里的任意类的任意方法。“..”出现在类名中时，后
面必须跟“*”，表示包、子包下的所有类。
execution(* *..service.*.*(..))
指定所有包下的 serivce 子包下所有类（接口）中所有方法为切入点
execution(public void com.bjpn.service.UserService.addUser(..))
~~~



### 非注解方式实现AOP

* 目标类：

~~~java
@Component
public class ATM {
    public void addMoney(){
        System.out.println("存储");
    }
}
~~~

* 增强类：

~~~java
@Component
public class Log {
    public void operationLog(){
        System.out.println("记录操作");
    }
    public void balanceLog(){
        System.out.println("记录余额");
    }
}
~~~

* 配置：

要在存款操作前记录操作，在存款操作后记录余额

~~~xml
<!--配置AOP-->
<aop:config>
    <!--配置切面-->
    <!--表示这个切面的增强类是log-->
    <aop:aspect ref="log">
        <!--在切面上配置切点-->
        <aop:pointcut id="addMoney" expression="execution(* com.bjpn.bean.*.addMoney(..))"/>
        <!--设置通知，在指定切点以指定通知方式调用指定方法-->
        <aop:before method="operationLog" pointcut-ref="addMoney"/>
        <aop:after method="balanceLog" pointcut-ref="addMoney"/>
    </aop:aspect>
</aop:config>
~~~

### 注解方式实现AOP

* 配置

~~~xml
<!--开启AOP注解-->
<aop:aspectj-autoproxy/>
~~~



* 目标类

~~~java
@Component("atm")
public class ATM {
    public void addMoney(){
        System.out.println("存储");
    }
}
~~~

* 增强类

~~~java
@Component
@Aspect
public class Log {
	//设置切点，需要再定义一个方法，当做切点的名称
    @Pointcut("execution(* com.bjpn.bean.*.addMoney(..))")
    public void addMoneyP(){}

    @After("addMoneyP()")
    public void operationLog(){
        System.out.println("记录操作");
    }
    @Before("addMoneyP()")
    public void balanceLog(){
        System.out.println("记录余额");
    }
}
~~~



# Spring事务管理

spring通过aop提供了事务管理

## maven依赖

我们通过mybatis的jdbc进行spring事务管理的示例：

首先需要引入mybatis，spring，spring-mybatis,mysql

~~~xml
<!--spring核心ioc-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
<!--mybatis依赖-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.6</version>
</dependency>
<!--mybatis和spring集成的依赖-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.1</version>
</dependency>
<!--mysql驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.17</version>
</dependency>
~~~

spring还依赖spring-tx ,spring-jdbc来进行事务：

~~~xml
<!--做spring事务用到的-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
~~~

## Spring提供事务行为

spring提供了7中事务行为，其中最常用：

* PROPAGATION_REQUIRED  支持当前事务，假设当前没有事务。就新建一个事务   最常用 增删改
* PROPAGATION_SUPPORTS  支持当前事务，假设当前没有事务，就以非事务方式运行  查询



## 非注解配置

~~~xml
<!--配置事务管理器类-->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--这里为事务管理器类提供数据源，数据源会在mybatis与spring整合时，由spring提供-->
    <property name="dataSource" ref=""/>
</bean>

<!--配置事务aop-->
<aop:config>
    <!--配置切点-->
    <aop:pointcut id="allMethodPointcut" expression="execution(* com.bjpn..service.*.*(..))"/>
    <!--配置通知器-->
    <aop:advisor advice-ref="txAdvice" pointcut-ref="allMethodPointcut"/>
</aop:config>

<!--配置事务传播行为-->
<tx:advice id="txAdvice">
    <tx:attributes>
        <tx:method name="add*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="save*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="edit*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="update*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="delete*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="remove*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="modify*" propagation="REQUIRED" rollback-for="Exception"/>
        <tx:method name="get*" propagation="SUPPORTS" read-only="true"/>
        <tx:method name="find*" propagation="SUPPORTS" read-only="true"/>
    </tx:attributes>
</tx:advice>
~~~



## 注解配置

~~~xml
<!-- 可通过注解控制事务 -->
<tx:annotation-driven transaction-manager="transactionManager" />
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="" />   
</bean>
~~~





~~~java
//标示当前类需要事务
@Transactional
@Service
public class UserServiceImpl implements UserService {
    @Override
     @Transactional(propagation = Propagation.REQUIRED,rollbackFor = {Exception.class})
    public boolean transferMoney(String code, String code1, double money) {
        //加钱  修改数据库
        //减钱  修改数据库
        //同时完成  业务才完成
        return false;
    }

    @Override
    //配置当前方法的事务  查询事务  可以有  也可以没有
    @Transactional(propagation = Propagation.SUPPORTS,readOnly = true)
    public void findAll() {

    }

    @Override
    //没有事务会创建事务  有多个事务会合并事务
    @Transactional(propagation = Propagation.REQUIRED,rollbackFor = {Exception.class})
    public void addMoney() {

    }
}
~~~

















