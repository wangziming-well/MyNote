# SQL语句

* SQL语句：Stuctured Query Language 结构化查询语句。
* SQL语句不依赖于任何平台，对所有的数据库是通用的。
* SQL具有查询、操纵、定义和控制关系型数据库的功能
* SQL是一个非过程性的语句，每个SQL执行完都有有一个具体的结果出现。

## SQL分类

* DDL：数据定义语言
* DML：数据处理语言
* DCL：数据控制语言
* DQL：数据查询语言



# 数据库的操作

~~~cmd
连接数据库
mysql （-h ip -P端口）-u username -p password
连接本机时可省略ip和端口
~~~

~~~sql
#查询数据库#
show databases;#查询所有的数据仓库
show create database 数据库名;#查询指定数据库创建规则

#创建数据库#
create database 数据库名; 
#创建时没有指定编码表，因此会使用安装数据库时默认的编码表。
create database 数据库名 character set 编码表名; 
#创建数据库会使用指定的编码表。
create database 数据库名 character set 编码表名 collate 排序规则; 
#使用指定的编码表同时还可以根据编码表指定排序规则。 规则查看MySQL_5.1 版本的API。

drop database 数据库名; #删除数据库

alter database 数据库名 character set 字符集 collate 比较规则;
# 修改数据库编码集或者比较规则

select database(); #查询正在使用的数据库

use 数据库名;#切换/使用数据库
~~~

# MYSQL的数据类型

~~~sql
# 字符型
varchar(列长)
char(列长)

# 数值型
tinyint
smallint
int
bigint
float
double

#逻辑形
BIT

#日期型
DATE 年月日
TIME 时分秒
DATETIME 年月日时分秒
TIMESTAMP 年月日时分秒（自动更新保存数据时的当前时间。）

# 大数据类型
BLOB 保存字节数据
TEXT 保存字符数据
~~~

# MySQL运算符

~~~sql
比较运算：相等 =   不等 <> 
		大于 > , &gt;
		小于 < , &lt;
		大于等于 >= , &gt;=
		小于等于 <= , &lt;=

逻辑运算： and or not 

区间判断： between ...and... (取闭区间)

列表取值：in(值，值，值)

模糊查询 like'pattern'   %表示任意字符串，_表示单个字符

null空判断: is null  和 is not null




~~~

# 表结构的操作

~~~sql
show tables; # 查看所有表

create table 表名(列名 类型，类名 类型...);#创建表

show create table 表名# 查看数据表信息 

drop table 表名;# 删除表

desc 表名;#查询表结构

# 表单创建时约束
列名 列的类型 unique; # 唯一约束
列名 列的类型 not null; # 非空约束
列名 列的类型 primary key; # 主键约束（唯一且非空）
列名 列的类型 auto_increment; #自增长

列名 列的类型 default 默认值# 设置默认值

#修改删除表结构
rename table 旧表名 to 新表名;# 修改表名
alter table 表名 add 列名 类型 约束;  # 增加列
alter table 表名 modify 列名 类型 约束;  # 修改现有列的类型和约束
alter table 表名 change 旧列名 新列名 类型 约束;  # 修改现有列名称 类型和约束
alter table 表名 drop 列名; #删除列
alter table 表名 character set 字符集;# 修改表字符集

~~~

# 表数据的操作

~~~sql
insert into 表名(列名，列名，列名......) values (值，值，值......);
# 插入数据
select * from 表名;
# 查看表中数据
update 表名 set 列名=值,列名=值.... where条件语句; 
# 修改表中数据
delete from 表名 where 条件语句；
#删除表中数据
delete from 表名 
# 删除表中所有数据
truncate table person;
# 删除表中所有数据 不可回滚 重置表的自增值

select * from 表名 where 查询条件; # 根据条件查询表中的所有数据
select 列名，列名... from 表名; # 查询指定列的所有数据
select 列名，列名... from 表名 where 查询条件; # 根据条件查询指定列的所有数据

select * from 表名 order by 列名 asc|desc ;
# 排序查询 asc 是升序,desc是降序

select 列名 as 别名,列名 as 别名,列名 as 别名.... from 表名 where 条件;
#给查询出来的列起别名,其中as可以省略

select distinct 列名 from 表名 where 条件;
#排重查询

select * from 表名 limit n; # 表示从0下标开始截取前N个数据
select * from 表名 limit n , m; # 表示从n下标开始截取m个数据，如果m超过最大下标，则返回n下标开始的所有数据。
~~~

# SQL中的函数

~~~sql
# 统计
select count(*)|count(列名) from 表名 where 条件;
    # count(*) ： 统计某一列的数据，包含null
    # count(列名)：统计指定列的数据，不包含null

# 求和
select sum(列名) from 表名 where 条件; 
#注意：null与任何数据相加都为0，sum（null）为0
ifnull(列名，值)
# 求平均值
select avg(列名) from 表名 where 条件;
# 最大值最小值
select max(列名),min(列名) from 表名 where 条件;
# 分组
select * from 表名 group by 列名;
#group by 它可以根据指定列对数据进行归类。如果这一列中有重复的数据会被合并成一个。
# having后面可以跟聚合函数，作用于where一样
~~~



# 多表设计

## 外键约束

* 外键： 在一个表中去引用另外一张表的主键作为该表的字段，这个字段被称为外键，一旦有了外键，表与表之间就产生了外键约束

* 作用：减少数据冗余，维护多表之间的数据完整性，减少垃圾数据

* 主表：主键被引用的表

* 从表：存在外键的表

* **必须保证从表的外键值在主表的主键值中存在**

* 语法：

    ~~~sql
    #表存在时：
    alter table 从表 add constraint 外键约束名 foreign key(从表的列) references 主表(主表的主键列)
    #表创建时；
    constraint 外键约束名 foreign key(从表的列) references 主表(主表的主键列)
    #直接在属性后：
    references 主表(主表的主键列)
    s
    #解除外键约束
    alter table 表名 drop foreign key 外键约束名;
    ~~~



## 级联操作

* 通过操作主表的数据，从而影响到从表的数据。

* **操作风险很大，一般默认不进行级联操作**

* 语法格式:

    ~~~sql
    #级联更新 ：
    外键约束语句 on update cascade;
    #级联删除 ：
    外键约束语句 on delete cascade;
    ~~~

    

## 数据库设计三大范式

* 第一范式：要求表的每个字段必须是不可分割的独立单元。
* 第二范式：要求每张表只表达一个意思，表的每个字段和表的主键有依赖
* 第三范式：要求每张表的主键之外的其他字段都只能和主键有直接决定的依赖



# 多表查询

## 内联查询

~~~sql
select * from 表名1,表名2 where 表名1.列名 = 表名2.列名;
select * from 表名1 inner join 表名2 on 条件;
~~~

## 外联查询

~~~sql
# 右外连接
select * from 表1 left outer join 表2 on 条件;
# 左外连接
select * from 表1 right outer join 表2 on 条件;
# 全连接
select * from 表1 full outer join 表2 on 条件; # 但是mysql数据库不支持此语法。 

#在sql语句全连接，其实就是左外链接和右外连接之和，并且使用union去掉重复的数据。
select * from 表1 left outer join 表2 on 条件 
union all 
select * from 表1 right outer join 表2 on 条件;


~~~

## SQL关联子查询

* 子查询：把一个SQL语句的查询结果当做另一个SQL语句查询的参数



# 索引

* 建表时创建索引：

    ~~~sql
    index(字段名称) # 普通索引 字段的值可以重复
    unique index(字段名称) #唯一索引 这个字段的值不能重复
    ~~~

* 组合索引

    ~~~sql
    index(字段1,字段2...)    
    # 组合索引的使用：组合索引存在最左原则，左侧的字段1如果如果在查询的时候使用则是有效索引，如果左侧的字段1没有使用，只是使用了字段2，那么索引也不会效果。
    ~~~

* 表创建后创建索引

    ~~~sql
    create index 字段名 on 表名(字段名);
    ~~~

    

    

# 事务

要求在逻辑上的一组（insert、update、delete）SQL语句，在执行时，要么全部成功，要么全部失败。

~~~sql
start transaction;#此语句后面的所有SQL语句都处在在事务中，更改的内容不会自动提交，需要手动提交
rollback；#事务的回滚，表示全部失败，事务结束，并且数据回复到开始之前的状态
commit;#事务的提交，表示全部成功，事务结束，数据更改
~~~





~~~sql
create table userdata(
	id int primary key auto_increment,
    code char(19) not null unique,
    phoneNumber char(11) not null unique,
    password char(6) not null,
    name varchar(8) not null,
    address varchar(16) not null,
    sex char(1) not null,
    account double not null default 0
)
~~~









