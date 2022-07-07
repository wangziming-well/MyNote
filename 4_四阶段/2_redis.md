# Redis简介

redis是非关系型数据库。

能处理集中高并发操作。

数据可以存储在内存中。

分布式数据库。

# Liunx的Redis操作

* 启动服务端：
    * `redis-server`前台启动，关闭命令窗口，服务器就关闭
    * `redis-server &`后台启动
    * `redis-server redis.conf &`加载配置启动
* 关闭服务器：
    * `redis-cli shtdown`
    * `kill -9 pid`

* 启动客户端：
    * `redis-cli [-h host] [-p port]`默认地址端口为127.0.0.1:6379

# 基础命令

* `ping`沟通命令，若返回PONG则表示redis服务正常运行
* `dbsize`查看当前数据库中key数目
* `select db`切换库命令
* `flushdb`删除当前库的数据
* `exit|quit`退出客户端
* `info`查看当前服务器的信息
    * all 全部Redis系统状态统计信息。
    * server	获取 server 信息
    * clients	获取 clients 信息，如客户端连接数等
    * memory	获取 server 的内存信息，包括当前内存消耗、内存使用峰值
    * persistence	获取 server 的持久化配置信息
    * stats	获取 server 的一些基本统计信息，如处理过的连接数量等
    * replication	获取 server 的主从配置信息
    * cpu	获取 server 的 CPU 使用信息
    * keyspace	获取 server 中各个 DB 的 key 的数量
    * cluster	获取集群节点信息，仅在开启集群后可见
    * commandstas	获取每种命令的统计信息


# Key命令

* `keys pattern`查找所有符合模式pattern的key
    * `*`匹配0-对个字符
    * `?`匹配单个字符
* `exists key [key...]`判断key是否存在，返回存在的key的数量
* `expire key seconds`设置key的生存时间
* `ttl key`查看key的生存时间
    * -1表示永远存在
    * -2表示不存在
* `type key`查看key的类型 none表示该key不存在
* `del key [key...]`删除指定的key，返回成功删除的key的数量



# 数据类型

## string

字符串类型时Redis中最基本的数据类型，能存储任何形式的字符串，包括二进制数据，序列化后的数据，JSON化的对象甚至是图片

* `set key value`

    设置字符串数据的KV

    * 若key存在，则覆盖value
    * 若key不存在，创建新数据

* `get key`

    获取指定字符串的key

    * 若key存在，返回对应的value
    * 若key不存在，返回nil

* `incr`

    将key中存储的数字值加1，只能对数值类型的string操作

    * 若key不存在，可以的值会被初始化为0再执行incr操作

* `decr`

    将key中存储的数字值减1，只能对数值类型的string操作

    * 若key不存在，可以的值会被初始化为0再执行decr操作

* `append key value` 

    追加字符串，返回新值的长度

    * 如果key存在，将value追加到旧值的末尾
    * 如果key不存在，则将key设置值为value

* `strlen`

    返回字符串长度，若key不存在返回0

* `getrange key start end`

    获取key中从start开始到end结束的子字符串

    * 负数表示从字符串的末尾开始，-1表示最后一个字符
    * start表示的位置必须在end表示位置之前

* `setrange key offset value`

    用value覆盖key的存储的值，从offset开始，不存在的key做空白字符串。返回修改后的字符串的长度

* `mset key value [key value ...]`

    批量添加字符串

* `mget key [key ...]`

    批量获取字符串key对应的值

## hash

redis哈希类型hash是一个string类型的field和value的映射表

* `hset key field value`

    将哈希表key中域field的值设为value

    * 若key不存在，则创建hash表，执行赋值
    * 若field存在，则覆盖vallue

* `hget key field`

    获取哈希表key中的field的值

    * 若key不存在或者field不存在返回nil

* `hmset key field value [field value ...]`

    批量设置哈希表的field-value

    * 若key不存在，创建空的hash表，执行hmset命令
    * 设置成功返回OK否则返回错误信息

* `hmget key field [field...]`

    批量获取哈希表field的值

* `hgetall key`

    获取哈希表中所有的域和值

* `hdel key field [field ...]`

    删除哈希表key中指定的域

* `hkeys key`

    查看哈希表key中所有的field

* `hvals key`

    查看哈希表key中所有的value

* `hexists key field`

    查看哈希表key中给定域field是否存在

    * 如果存在返回1
    * 如果不存在返回0

## list

简单的字符串列表

* `lpush key value [value...]`

    从列表key表头依次插入指定value

* `rpush key value [value...]`

    从列表key队尾依次插入指定value

* `lrange key start stop`

    获取列表key指定范围的值

* `lindex key index`

    获取列表key指定下标的值

* `llen key`

    获取列表key的长度

* `lrem key count value`

    移除列表key中指定value ，count次

    * count为0 全部移除
    * count为正，从表头开始移除
    * count为负，从表未开始移除

* `lset key index value`

    设置列表key指定下标位置的值

* `linsert key before|after pivot value`

    在指定的第一个pivot元素的头或尾插入指定的值

## set

是string类型的无序集合，成员唯一



* `sadd key member [member ...]`

    将一个或者多个member元素添加到集合key中

    * 如果没有key则创建集合
    * 如果member已经存在，则不会再加入
    * 返回添加到集合的新元素的个数

* `smembers key`

    查看指定集合key的所有成员，如果key不存在则视为空集合

* `sismember key member`

    判断指定成员member是否在指定集合key中

    * 如果在，返回1
    * 如果不在，返回0

* `scard key`

    返回集合的长度

* `srem key member [member...]`

    删除集合key的指定成员

    返回成功删除的数量

* `srandmember key [count]`

    随机返回指定数量的集合key的成员，count默认为1

* `spop key [count]`

    随机弹出指定数量的集合key的成员，count默认为1

## zset

zset 的每一个元素都会关联一个分数（分数可重复，必须是数值类型）

redis通过分数来为集合中的成员进行从小到大排序



* `zadd key score member [score member...]`

    将指定的member元素和对应分数scores加入到有序集合key中

    如果key不存在，则创建有序集合

    返回新添加的元素个数

* `zrange key start stop [withscores]`

    顺序查询有序集合key，start，stop指定范围，可以指定是否显示成员分数

* `zrevrange key start stop [withscores]`

    倒序查询有序集合key

* `zrem key member[member]`

    删除指定的有序集合key成员

    返回成功删除的成员数量

* `zcard key`

    返回指定有序集合key的大小

* `zrangebyscore key min max [withscores] [limit offset count]`

    按照分数顺序查询指定范围的有序集合key的成员

    可以指定是否显示分数

    可以指定是否分页

    * min max 默认是闭区间范围
    * 可在数字前加`(`指定开区间
    * `+inf` `-inf`表示最大数和最小数

* `zrevrangebyscore key min max [withscores] [limit offset count]`

    按照分数倒序查询指定范围的有序集合key的成员

* `zcount key min max`

    查询指定分数范围内成员的数量





# Redis事务

* `multi`

    标记一个事务的开始。事务内的多条命令会按照先后顺序被放进一个队列中

* `exec`

    执行所有事务块内的命令，返回事务内所有执行语句的结果，事务被打掉返回nil

* `discard`

    取消事务

* `watch key [key...]`

    监视指定的key，若事务执行之前，监视的key有被其他命令改动， 事务将被打断

* `unwatch`

    取消监视

# 持久化

将数据备份到硬盘中，防止服务器关机或者重启导致内存redis数据丢失

## RDB

Redis Database 

将内存中的数据集快照写入磁盘，数据恢复时将快照文件直接读到内存中

自动RDB只需要在redis.conf文件中配置即可，默认配置时启用的：

* `save <seconds><changes>`设置生成RDB文件的时间策略，含义是，数据在指定的时间范围内变动指定次数就保存一次RDB文件
* `dbfilename`设置RDB的文件名，默认为dump.rdb
* `dir`设置RDB文件的存储位置，默认为./当前目录

也可以手动命令保存：

* `save`保存
* `bgsave`后台保存



优缺点：

* 由于存储的是数据快照文件，恢复数据很方便，也比较快 ，容灾备份
    缺点： 
* 会丢失最后一次快照以后更改的数据。如果你的应用能容忍一定数据的丢失，那么使用 rdb 是不错的选择；如果你不能容忍一定数据的丢失，使用 rdb 就不是一个很好的选择。 
* 由于需要经常操作磁盘，RDB 会分出一个子进程。如果你的 redis 数据库很大的话，子进程占用比较多的时间，并且可能会影响 Redis 暂停服务一段时间（millisecond 级别），如果你的数据库超级大并且你的服务器 CPU 比较弱，有可能是会达到一秒。 



## AOP

Append-only File Redis每次接受到一条改变数据的命令时，它将把该命令写到一个AOF文件中，当Redis重启时，它通过执行AOF文件中的所有命令来恢复数据

配置redis.conf:

* `appendonly`是否开启aof持久化，默认为no，改为yes开启

* `appendfilename`指定AOF文件名，默认文件名为appendonly.aof

* `dir`指定RDB和AOF文件存放的目录，默认是./

* `appendfsync`配置aof文件写命令数据的策略：

    * `no`不主动进行同步操作，完全交由操作系统来做(每30s一次)
    * `always`每次执行写入修改都会执行同步
    * `everysec`每秒执行一次同步操作

* `auto-aof-rewrite-min-size`允许重写的最小AOF文件大小，默认为64M

    当aof文件大于64M时，开始整理aop文件，去掉无用的操作命令(只保存对key的最后一次修改操作)

优缺点：

* append-only 文件是另一个可以提供完全数据保障的方案； 

* AOF 文件会在操作过程中变得越来越大。比如，如果你做一百次加法计算，最后你只会在数据库里面得到最终的数值，但是在你的 AOF 里面会存在 100 次记录，其中 99 条记录对最终的结果是无用的；但 Redis 支持在不影响服务的前提下在后台重构 AOF 文件，让文件得以整理变小 

* 可以同时使用这两种方式，redis默认优先加载aof文件（aof数据最完整）



# Redis主从复制

为了避免单点故障，我们需要将数据复制多份部署在多台不同的服务器上

redis可以指定保存相同数据的服务器之间的主从关系：

* master主服务器负责写入数据，同时把写入的数据实时同步到从服务器

* slave从服务器只能用于读数据，无法写数据

设置主从服务器方法：

* 如果没有声明指定，默认为主服务器
* 指定从服务器可以的方法：
    * 配置文件中：设置`slaveof <master-ip> <master-port>`
    * 启动服务器时：加上属性`--slaveof <master-ip> <master-port>`
    * 客户端命令：
        * `slaveof no one`提升自己为master
        * `slaveof <master-ip> <master-port> `

# Sentinel

sentinel哨兵提供主从复制模式的故障转义的的自动化处理

## 原理

Redis Sentinel是运行在特殊模式下的Redis服务器

有三个主要任务：

* 监控：Sentinel不断检查主服务器和从服务器是否按照预期正常工作，

    每隔固定时间sentinel会请求主服务器，如果没有收到主服务的正常响应，则报告异常

* 提醒：被监视的Redis出现问题时，Sentinel会通知管理员或其他应用程序

* 自动故障转移：监控的主Redis不能正常工作，Sentinel会开始进行故障迁移操作。

    将一个从服务器升级新的主服务器。让其他从服务器挂到新的主服务器。同时向客户端提供新的主服务器地址

Sentinel分布式系统：

* 如果只有一个Sentinel，那么Sentinel出现问题就无法监控。所以需要多个哨兵，组成Sentinel网络。一个健康的sentinel至少有三个Sentinel应用。彼此在独立的物理机器或虚拟机
* 监控同一个Master的Sentinel会自动连接，组成一个分布式的网络，互相通信并彼此蒋欢关于被监控服务器的信息
* 当一个 Sentinel 认为被监控的服务器已经下线时，它会向网络中的其它 Sentinel 进行确认，判断该服务器是否真的已经下线 
* 如果下线的服务器为主服务器，那么 Sentinel 网络将对下线主服务器进行自动故障转移，通过将下线主服务器的某个从服务器提升为新的主服务器，并让其从服务器转移到新的主服务器下，以此来让系统重新回到正常状态 
* 下线的旧主服务器重新上线，Sentinel 会让它成为从，挂到新的主服务器下 

## 实现

配置sentinel.conf文件：

~~~python
#sentinel自己的接口:
port <port>
#sentinel要监视的master:
sentinel monitor <name> <masterIP> <masterPort> <Quorum>
# quorum 表示投票数，当有超过该数量的哨兵认为服务器已经下线，才会判断下线
~~~

启动sentinel服务器：

~~~python
redis-sentinel sentinel.conf
~~~

# 安全

* 设置密码

    去掉redis.conf 中的requirepass foobared 的注释

    访问有密码的Redis两种方式：

    * 连接到客户端后，使用命令 `auto password`
    * 连接客户端时，`redis-cli -a password`

* 绑定ip

    redis.conf 中的bind字段

* 修改端口

    redis.conf中的port字段



# Jedis

jedis是java连接redis的官方推荐包，几乎所有的方法都与redis命令一致

## 依赖

~~~xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>3.3.0</version>
</dependency>
~~~



## 获取对象

* 通过构造方法：

~~~java
Jedis jedis = new Jedis("192.168.134.128",6379);
~~~

* 通过pool

~~~java
JedisPoolConfig config = new JedisPoolConfig();
//设置连接池最大连接数量
config.setMaxTotal(10);
//设置连接池最大空闲连接数
config.setMaxIdle(3);
//提前检查Jedis对象，让获取的Jedis一定是可用的
config.setTestOnBorrow(true);
//创建Jedis连接池
JedisPool pool = new JedisPool(config, "192.168.134.128", 6379, 6 * 1000, "123456");
Jedis jedis = pool.getResource();
~~~

## 对象方法

### 键方法

* `flushAll() ` 清空所有数据库数据
* `flushDB()`	清空当前数据库数据
* `boolean exists(String key)`	判断某个键是否存在
* `set(String key,String value)`	新增键值对
* `Set<String> keys(String pattern)`	返回匹配的key
* `del(String key)`	删除键为key的数据项	
* `expire(String key,int i)`	设置键为key的过期时间为i秒	
* `int ttl(String key)`	获取建委key数据项的剩余时间（秒）	
* `persist(String key)`	移除键为key属性项的生存时间限制	
* `type(String key)`	查看键为key所对应value的数据类型	



### 字符串类型方法

* `set(String key,String value)`	增加（或覆盖）数据项
* `setnx(String key,String value)`	不覆盖增加数据项（重复的不插入）
* `setex(String ,int t,String value)`	增加数据项并设置有效时间
* `del(String key)`	删除键为key的数据项
* `get(String key)`	获取键为key对应的value
* `append(String key, String s)`	在key对应value 后边扩展字符串 s
* `mset(String k1,String V1,String K2,String V2,…)`	增加多个键值对
* `String[] mget(String K1,String K2,…)`	获取多个key对应的value
* `del(new String[](String K1,String K2,.... ))`	删除多个key对应的数据项
* `String getSet(String key,String value)`	获取key对应value并更新value
* `String getrange(String key , int i, int j)`	获取key对应value第i到j字符 ，从0开始，包头包尾



### 哈希类型方法

* hmset(String key,Map map)	添加一个Hash
* hset(String key , String key, String value)	向Hash中插入一个元素（K-V）
* hgetAll(String key)	获取Hash的所有（K-V） 元素
* hkeys（String key）	获取Hash所有元素的key
* hvals(String key)	获取Hash所有元素 的value
* hincrBy(String key , String k, int i)	把Hash中对应的k元素的值 val+=i
* hdecrBy(String key,String k, int i)	把Hash中对应的k元素的值 val-=i
* hdel(String key , String k1, String k2,…)	从Hash中删除一个或多个元素
* hlen(String key)	获取Hash中元素的个数
* hexists(String key,String K1)	判断Hash中是否存在K1对应的元素
* hmget(String key,String K1,String K2)	获取Hash中一个或多个元素value



### 列表类型方法

* `lpush(String key, String v1, String v2,....)`	添加一个List , 注意：如果已经有该List对应的key, 则按顺序在左边追加 一个或多个
* `rpush(String key , String vn)`	key对应list右边插入元素
* `lrange(String key,int i,int j)`	获取key对应list区间[i,j]的元素，注：从左边0开始，包头包尾
* `lrem(String key,int n , String val)`	删除list中 n个元素val
* `ltrim(String key,int i,int j)`	删除list区间[i,j] 之外的元素
* `lpop(String key)`	key对应list ,左弹出栈一个元素
* `rpop(String key)`	key对应list ,右弹出栈一个元素
* `lset(String key,int index,String val)	`修改key对应的list指定下标index的元素
* `llen(String key)`	获取key对应list的长度
* `lindex(String key,int index)`	获取key对应list下标为index的元素
* `sort(String key)`	把key对应list里边的元素从小到大排序 

### 集合类型方法

* `sadd(String key,String v1,String v2,…)`	添加一个set
* `smenbers(String key)`	获取key对应set的所有元素
* `srem(String key,String val)`	删除集合key中值为val的元素
* `srem(String key, Sting v1, String v2,…)`	删除值为v1, v2 , …的元素
* `spop(String key)`	随机弹出栈set里的一个元素
* `scared(String key)`	获取set元素个数
* `smove(String key1, String key2, String val)`	将元素val从集合key1中移到key2中
* `sinter(String key1, String key2)	`获取集合key1和集合key2的交集
* `sunion(String key1, String key2)`	获取集合key1和集合key2的并集
* `sdiff(String key1, String key2)`	获取集合key1和集合key2的差集

### 有序集合方法

* `zadd(String key,Map map)`	添加一个ZSet
* `hset(String key,int score , int val)`	往 ZSet插入一个元素（Score-Val）
* `zrange(String key, int i , int j)`	获取ZSet 里下表[i,j] 区间元素Val
* ` zrangeWithScore(String key,int i , int j)`	获取ZSet 里下表[i,j] 区间元素Score - Val
* `zrangeByScore(String , int i , int j)`	获取ZSet里score[i,j]分数区间的元素（Score-Val）
* `zscore(String key,String value)	`获取ZSet里value元素的Score
* `zrank(String key,String value)`	获取ZSet里value元素的score的排名
* `zrem(String key,String value)`	删除ZSet里的value元素
* `zcard(String key)`	获取ZSet的元素个数
* `zcount(String key , int i ,int j)`	获取ZSet总score在[i,j]区间的元素个数
* `zincrby(String key,int n , String value)`	把ZSet中value元素的score+=n

### 数的方法

* `incr(String key)`	将key对应的value 加1
* `incrBy(String key,int n)`	将key对应的value 加 n
* `decr(String key)`	将key对应的value 减1
* `decrBy(String key , int n)`	将key对应的value 减 n

### 事务方法

* `multi()`开启事务
* `exec()`执行事务
