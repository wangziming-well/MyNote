# 关键字和标识符

关键字：被Java语言赋予特殊含义，用作专门用途的的字符串

* 特点：所有全部都是小写

标识符：表示起一定标识作用的符号。标识作用的符号是指程序中定义的名称。

* 命名规则：
    * 取值范围：`a-z` `A-Z` `0-9` `_` 和`$`
    * 数字不能开头
    * 不能直接使用关键字或者保留字，但是可以包含关键字和保留字
    * 严格区分大小写，长度无限制
    * 标识符不可以包含空格
* 规范：
    * 包名：多单词组成时所有字母都小写
    * 类名，接口名：多单词组成时，所有单词的首字母大写
    * 变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写
    * 常量名：所有字母都大写。多单词时每个单词用下划线连接

# 注释

作用：

* 对代码翻译解释

* 注释内容不会被编译运行

注释符号：

1. 单行注释：`//注释内容`

2. 多行注释：`/*  注释内容 */`

3. 文档注释：`/** */`

    ​		文档注释可以添加格式：

    ​				`@变量名 变量值`

    ​		例如:

    ​				`@author 	xxx`

    ​				`@version	xxx`

# 字面量

    1. 数值型：整数 小数

    2. 布尔型：`true`、 `false` 

    3. 字符型：

     * 用单引号描述`''`
     * 只能描述单个字符，如'a','c','0'

    4. 字符串类型：

     * 描述多个字符，包含的字符个数的范围：[0,+∞）
     * 用双引号描述`""`

    5. 空值：
     * 关键字`null`
     * 含义：不存在


# 变量

它是内存中的一块存储区域（空间），有数据类型的限制

可以存入匹配类型的数据，并且根据需求随时改动其内容

变量名也是标识符之一,需要满足标识符的规则和规范

## 特点

1. 变量是一款容器 ==> Java内存层面
2. 只能存储单个数据

## 定义格式

* 声明同时初始化：

    ~~~java
    数据类型 变量名 = 初始化值；
    ~~~

* 先声明后初始化：

    ~~~java
    数据类型 变量名；
    变量名 =初始化值；
    ~~~

# 数据类型

Java中数据分为基本数据类型与引用数据类型

## 基本数据类型

* 整数型：

    | 又称   | 关键字 | 占用内存      | 取值范围         |
    | ------ | ------ | ------------- | ---------------- |
    |        | byte   | l byte (8bit) | [-2^7^,2^7^-1]   |
    | 短整型 | short  | 2byte (16bit) | [-2^15^,2^15^-1] |
    | 整型   | int    | 4byte (32bit) | [-2^31^,2^31^-1] |
    | 长整型 | long   | 8byte (64bit) | [-2^63^,2^63^-1] |

    **注意**：由于int是被主要使用的整数类型，所以程序中定义的整数型字面量全部都是默认类型int。

    整数型字面量属于默认类型int，所以在将整数型字面量赋值给长整型时，需要在数字末尾显式地标记L或l，告诉编译器这个字面量为长整型：

    ~~~java
    long l = 10000000000L
    ~~~


* 浮点型：

    | 类型         | 关键字 | 占用内存 |
    | ------------ | ------ | -------- |
    | 单精度浮点数 | float  | 4byte    |
    | 双精度浮点数 | double | 8byte    |

    **注意**：由于double是被主要使用的浮点类型，程序中定义的浮点型字面量全部都是默认类型double。

    浮点型字面量属于默认类型double，所以在将double浮点型字面量赋值给float浮点型时，需要在数字的末尾显式的标记F或f，告诉编译器这个字面量为float型：

    ~~~java
    float d = 3.14f
    ~~~

**注意**：浮点类型开辟空间大小远远大于整数型

* 布尔类型：

    ​	关键字：boolean

    ​	取值范围：true false

* 字符类型：

    ​	关键字：char

    ​	符号：单引号

    ​	特点：只能描述单个字符

    ​				可以描述转义字符

    ​				每个字符都对应一个编码值

    ​	需要记住的3个编码值：

    | 字符 | 编码值 |
    | ---- | ------ |
    | ‘0’  | 48     |
    | ‘A’  | 65     |
    | ‘a'  | 97     |

    常用转义字符：

    | 字符 | 含义       |
    | ---- | ---------- |
    | \\"  | 表示双引号 |
    | \\'  | 表示单引号 |
    | \\t  | 表示制表符 |
    | \\n  | 表示换行符 |

## 基本数据类型的类型转换

* 自动类型转换（隐式类型转换），简称：自转

    * 特点：小容量类型 ->大容量类型 

        ​			或者当**字面量**大容量类型->小容量类型不发生精度损失时

    * 格式：

    ~~~java
    大容量数据类型 变量名2 = 变量名1;
    小容量数据类型 变量名3 = 字面量;
    ~~~

* 强制类型转换，简称：强转

    * 特点：大容量类型 ->小容量类型
    * 要求：需要显式地定义强制类型转换符：（需要被转换成的数据类型）
    * 格式:

    ~~~java
    小容量数据类型 变量名2 = （需要被转换成的数据类型）变量名1;
    ~~~

    **注意**：强制类型转换有精度丢失的风险

* 实例：

~~~java
int i = 200;
float f = i; //此处发生自动类型转换(浮点型的存储空间远远大于整型)
    
long 1 = 600L;
float f1 = l; //此处发生自动类型转换
~~~

* 类型转换底层流程图：

![](..\img\数据类型转换.png)

## 引用数据类型

Java中引用数据类型有数组、类、接口、枚举等。这里只介绍数组

### 数组

* 概念：

    是一块连续的存储空间，内部有许多个小空间，有数据类型的限定，可以存入一组匹配类型的数据，根据需要可以改动小区域中的数据。

* 特点：

    可以存储一组同类型（可以多态）的数据，方便日后的维护和管理。解决了变量只能存储单个数据的局限性

* 定义格式：

    * 静态初始化：声明定义数组，创建数组对象以及为数组元素赋值同时进行。

        ~~~JAVA
        数据类型 [] 数组名 = new 数组类型[]{a1,a2,...an}
        ~~~

        简化形式：

        ~~~java
        数据类型 [] 数组名 = {a1，a2,..,an}
        ~~~

    * 动态初始化：声明，创建，赋值分开进行

        ~~~java
        数据类型[] 数组名 =new 数据类型[容量]
        ~~~
    
* 数组元素默认值：

    * 整数型：0
    * 浮点型 ：0.0
    * 布尔型：false
    * 字符型：空白字符
    * 引用类型：null

* 堆内存：

    * 特点：只要是new出来的对象都在堆中

        ​			堆中的对象都有地址值

        ​			对象中的区域空间都有默认值

    基本类型变量，存储在基本类型空间，内部存储的都是常量值

    引用类型变量，存储在引用类型空间，内部存储的都是对象地址值

    引用数据类型变量可以存储地址值，也可以存储null值；基本类型变量不可以

* 数组内存解析：

    * 是在堆内存中的
    * 有地址，在栈空间中存储的是地址
    * 如果在堆空间中的对象没有指针指向它，那么它会被回收

    ~~~java
    int [] arr = new int [4];
    int [] arr2 = arr;  //进行浅拷贝
    arr = null          //数组空间不会被回收，因为arr2仍指向它
    ~~~

* 数组的弊端

    * 数组的长度一旦确定无法改变

* 普通常量值传递和引用地址值传递

    * 普通常量值传递：将数据拷贝一份给方法的形参位置

        改动数据，是暂时的，方法弹栈后，原数据不变

    * 引用地址值传递：将对象地址拷贝一份给到形参位置

        改动对象数据，是永久的，方法弹栈后改动任有效

### 二维数组

定义格式：

* 静态初始化

    ~~~java
    数据类型[][] 数组名 = new 数据类型 [][] {一维数组对象，...，}
    ~~~

* 动态初始化

    * 模板一：

        ~~~java
        数据类型 [][] 数组名 =new 数据类型 [一维数组个数][一维数组的元素个数]
        ~~~

    * 模板二：

        ~~~java
        数据类型 [][] 数组名 =new 数据类型[一维数组个数][]
        ~~~

        关联一位数组对象，存放的是地址；

# 运算符

## 算数运算符

* 一元运算：

    | 运算符 | 运算                             | 实例                   | 结果              |
    | ------ | -------------------------------- | ---------------------- | ----------------- |
    | ++     | 自增（前），先（自增）运算再取值 | a = 3;<br />b = ++a;   | a =4<br />b = 4   |
    | ++     | 自增（后），先取值再（自增）运算 | a = 3;<br />b = a ++； | a = 4<br />b = 3  |
    | --     | 自减（前），先（自减）运算再取值 | a = 3;<br />b = --a;   | a = 2<br />b = 2  |
    | --     | 自减（后），先取值再（自减）运算 | a = 3;<br />b = a --   | a  = 2<br />b = 3 |

* 二元运算： **+  -  *  /  %**

    * 加符号 ：

        * 拼接操作：当加号两边至少有一个是字符串型（双引号修饰的）时，加号将进行拼接操作，结果为一个更长的字符串型

        * 运算操作：当加号两边都不是字符串类型时（即使是字符型）时，加号将进行运算操作。

            当进行的运算操作中有字符型时，编译器将对字符的编码进行运算

    * 除法运算：如果运算符两侧的数据类型都是整数型，那么最终结果会执行取整操作，向0取整

    ~~~java
    9 / 2;   // 结果为4
    (-9)/2   //结果为 -4
    ~~~

    想要保留小数，就将除法的其中一个数设为浮点型

    ~~~java
    9 *1.0 / 2 //结果为4.5
    ~~~

    * ***取模***（余）：

        结果的正负号和被模数保持一致

        运算过程,对整型数a,b 来说， a mod b:

        * 求整数商：c = [a/b] 这里的取整是向零取整
        * 计算模(余)： r = a - c * b
    
* 算数运算符两侧数据类型不一致时，绝大多数情况下取大容量数据类型

    但有特殊情况：

    ​		byte 和 byte 之间做运算 结果为int

    ​		short 和 short 之间做运算 结果为int

    ​	    byte 和 short 之间做运算 结果为int

    ​		char 和 char 之间做运算 结果为int

* 比较运算符： `>  >=  <  <=  ==  !=`

​                   值都是布尔值

## 混合赋值运算符

符号：` +=  -=  *=  /=  %= `

~~~java
byte b = 100;
b += 500;  //不改变b原本的数据类型的举出上进行运算’jvm提供一个隐式的强制类型转换，所以结果为88
~~~

特点：在不改变数据原本数据类型的前提下，进行相关的操作

## 逻辑运算符

参与逻辑运算的表达式都是布尔类型，结果也是布尔类型

* 与操作：       
    * 含义：一假即假
    * 符号
        * 逻辑操作：`&`  
        * 短路操作：`&&`
    * 敏感条件：`false `
* 或操作：
    * 含义：一真即真
    * 符号:
        * 逻辑操作：`|` 
        * 短路操作：`||`
    * 敏感条件：`true `

* 逻辑操作和短路操作：
    * 逻辑操作 顺序执行，即使找到了第一个满足了逻辑运算的敏感条件的表达式，也会执行后续表达式
    * 短路操作 顺序执行，只要找到了第一个满足了逻辑运算的敏感条件的表达式，就不会执行后续的表达式
    * 短路操作比逻辑操作更安全也更高效，在后续学习和开发下，主要使用短路操作

* 异或操作：
    * 含义：相异为真
    * 符号：`^`
* 非操作：
    * 含义：取反
    * 符号：`!`

## 三元/三目运算符

* 格式 ：

    ~~~java
     条件表达式 ? 表达式1 : 表达式2;
    ~~~

* 执行流程：

    * jvm先执行条件表达式；
    * 如果条件表达式的结果为true，就执行表达式1，并且将表达式1的执行结果作为整个三目运算的最终结果；
    * 如果条件表达式的结果为false，就执行表达式2，并且将表达式2的执行结果作为整个三目运算的最终结果；

# 流程控制语句

顺序结构、判断结构、选择结构、循环结构

## 判断结构

* 格式一：

~~~java
if(假){
    //...
}
~~~

* 格式二：

~~~java
if(假){
    //...
}否则{
    //...
}
~~~

* 格式三：

~~~java
if(f){
    //...
}else if(t){
    //...
}else if(t){
    //...
}else{
    //...
}
~~~

## 选择结构

格式：

~~~java
swithc(expression){
    case value1:
        //语句
    case value2:
    	//语句
    default:
    	//语句
   
}
~~~

注意事项：

* 绝大多数情况下，每个case的最后位置都需要定义break，防止case穿透现象

* 从语法角度上：

    default是可有可无的，并且位置是可以随意的

* 从使用角度上：

​			default一定会被定义，并且只会被定义在最后位置

* default永远是case都不满足表达式值时，才会被执行

## 循环结构

* 四要素：

    * 初始化条件

    * 循环条件

    * 迭代条件

    * 循环体

### while循环

* 格式一

~~~java
while(条件表达式){
    //...  
}
~~~

* 格式二

~~~java
do{
    //...
}while(条件表达式)；
~~~

**注意**：while行后面必须有分号

**注意**：dowhile循环先执行循环体，再执行循环条件 

所以dowhile循环至少会执行一次循环体

### for循环

* 普通for循环

~~~java
for ( 初始化 ; 条件表达式 ; 迭代条件 ){
    //...
}
~~~

* 增强for循环

~~~java
for( 定义变量 : 容器对象){
    //...
}
~~~

容器对象必须实现Iterable接口

### 循环结构的关键字

在循环结构中：

* `break`：立即结束循环

* `continue`：结束当此循环，继续下一次循环

**注意**：break continue 默认只控制所在的最近的循环的流程

可以使用标签技术：

~~~java
标签名：for(){
    for(){
        break 标签名；
    }
}
~~~
