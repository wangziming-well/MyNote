## Java 语言的由来

* 1995年诞生
* 1996年发布第一版jdk
* 2008年：SUM公司收购Mysql公司
* 2009年：Oracle公司收购了SUM公司 

## Java 语言的特点

* 开源免费
* 跨平台性（可移植性）
* 垃圾回收机制

## 跨平台性的原理

JVM ：Java 虚拟机

## JDK JRE JVM

JVM（Java Virtual Machine）：Java虚拟机

JRE(Java Runtime Environment): Java运行环境：JVM +核心类库

JDK(Java Development Kit):Java开发工具包 ：JER +开发的指令集/工具集

如果仅仅想要Java程序，安装JRE即可

如果想进行Java开发，需要JDK

![](D:\Data\Learning\Java\笔记\img\JVM JER JDK关系图.png)



## 第一个Java程序

执行Java程序需要经历2个阶段：

* 阶段一：编译 通过javac.exe将程序语言(.java称为java源文件)编译成机器语言（.class又被称为类文件、字节码文件、二进制文件、机器码文件）
* 阶段二：运行 通过java.exe执行.class文件（执行命令时不能加后缀.class）

~~~java
class Demo{
    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
~~~

注意：

1. Java语言严格区分大小写
2. Java程序绝大多数情况下不是以大括号结尾就是以分号结尾
3. Java程序内容一旦进行改动，必须重新进行编译操作（javac的行为）

4. Java程序中的标点符号都是英文输入法下的

5. 在一个Java源文件中，public可以修饰类，但只能修饰一个类，而且类名必须和文件名一致



