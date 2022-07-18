# 函数式接口

* 定义：有且只有一个抽象方法的接口
* 可以用注解`@FunctionalInterface`来检测

* 常用函数式接口
    * Runnerable:线程任务接口
    * FilenameFilter：文件名过滤器
    * FileFileter：文件对象过滤器
    * Comparator：比较器

# Lambda表达式

* 用于优化函数式接口的匿名内部类的使用

* 本质是用更简单的方法重写函数式接口的抽象方法

* 语法格式

    ~~~java
    (形参列表)->{重写抽象方法的方法体}
    ~~~

    

* Lambda表达式省略格式：
    * ()中的数据类型可以省略
    * ()中有且仅有一个参数是，()可以省略
    * {}中只有一条语句时， `return {} ;`可以省略[必须一起省略]

* 好处：语句简单直接
* 弊端：可读性不高



# Stream流中的函数式接口

## Predicate

* 表示一个参数的谓词（布尔值函数）。 

* 抽象方法：

    boolean `test(T t)`  ：在给定的参数上计算这个谓词。 
    
* 默认方法

    * `default Predicate<T> and(Predicate<? super T> other) `
        返回一个由谓词表示短路逻辑和谓词和另一个。  
    * `default Predicate<T> negate() `
        返回一个表示该谓词的逻辑否定的谓词。  
    * `default Predicate<T> or(Predicate<? super T> other) `
        返回一个由谓词表示短路逻辑或该谓词和另一个。  



## Supplier

* 表示结果的供应商。 
* 抽象方法：`T get() `：得到一个结果。 

## Consumer

* 表示接受一个输入参数，并返回没有结果的操作。

* 抽象方法：

    `void accept(T t)`  在给定的参数上执行此操作。

* 默认方法：  

    `default Consumer<T> andThen(Consumer<? super T> after) `
    返回一个由 Consumer执行此操作，在序列，其次是 after操作。  

## Function<T,R>

* 表示接受一个参数并产生结果的函数。 

* 抽象方法：

    `R apply(T t) ` 将此函数应用于给定的参数。  

* 默认方法：

    `default <V> Function<V,R> compose(Function<? super V,? extends T> before) `
    返回一个由功能，首先应用 before函数的输入，然后将该函数的结果。  



# Stream接口

JDK8最重要的新特性之一。

可以操作一系列元素。用于操作集合和数组

模拟流水线

流只能用一次，且不改变集合和数组的原有元素



## 获取Stream流对象

* 集合获取Stream流：

    Collection接口中有Stream stream()返回单列集合的流对象

* 数组获取Stream流

    Arrays数组工具类中的

    * Stream stream(arr)
    * Stream stream(arr,startIndex,endIndex)

* 数据获取Stream流

    Stream接口中有静态方法Stream of(....)



## 成员方法



### 延迟方法

Stream<T> filter(Predicate<? super T> predicate) 
返回由该流的元素组成的流，该元素与给定的谓词匹配。  

Stream<T> limit(long maxSize) 返回由此流的元素组成的流，截短长度不能超过 maxSize 。

Stream<T> skip(long n) 在丢弃流的第一个 n元素后，返回由该流的剩余元素组成的流。 

<R> Stream<R> map•(Function<? super T,? extends R> mapper) 返回由给定函数应用于此流的元素的结果组成的流。 

static <T> Stream<T> concat•(Stream<? extends T> a, Stream<? extends T> b) 创建一个懒惰连接的流，其元素是第一个流的所有元素，后跟第二个流的所有元素。  

Stream<T> parallel() 
返回一个并行的等效流。 

### 终结方法

void forEach(Consumer<? super T> action) 
对该流的每个元素执行一个动作。  

long count() 返回此流中的元素数。  
