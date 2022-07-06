# IOStream流概述与继承体系

基于IO流的和数据的特点，IOStream有四个顶层的父类：

* java.io.OutputStream：字节输出流顶层父类，所有和字节相关的输出流都是它的子类。

* java.io.InputStream：字节输入流顶层父类，所有和字节相关的输入流都是它的子类。

* java.io.Writer：字符输出流顶层父类，所有和字符相关的输出流都是它的子类。

* java.io.Reader：字符输入流顶层父类，所有和字符相关的输入流都是它的子类。

继承树：

* OutputStream
    * FileOutputStream
    * ObjectOutputStream
    * FilterOutputStream
        * BufferedOutputStream
        * PrintStream
* InputStream
    * FileInputStream
    * ObjectInputStream
    * FilterInputStream
        * BufferedInputStream
    * SequenceInputStream
* Reader
    * BufferedReader
    * InputStreamReader
        * FileReader 

* Writer
    * BufferedWriter
    * OutputStreamWriter
        * FileWriter 
* RandomAccessFile

# OutputStream

## 描述

java.io.OutputStream: 字节输出流顶层抽象父类，所有和字节相关的输出流都是它的子类。

## 成员方法

*  void close() 

关闭此输出流并释放与此流有关的所有系统资源。 

* void flush()

刷新此输出流并强制写出所有缓冲的输出字节。 

* void write(byte[] b)

将 b.length 个字节从指定的 byte 数组写入此输出流。 

* void write(byte[] b, int off, int len)

将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。 

* abstract  void write(int b)

将指定的字节写入此输出流。 



# FileOutputStream

## 描述

java.io.FileOutputStream：文件字节输出流，用于将字节数据写入到本地文件中。

## 构造方法

* FileOutputStream(File file)
    创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 
* FileOutputStream(File file, boolean append) 
    创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 
* FileOutputStream(FileDescriptor fdObj) 
    创建一个向指定文件描述符处写入数据的输出文件流，该文件描述符表示一个到文件系统中的某个实际文件的现有连接。 
* FileOutputStream(String name)
    创建一个向具有指定名称的文件中写入数据的输出文件流。 
    *  如果指定的路径存在但是文件不存在则自动创建文件
    * 如果指定的路径不存在则抛出：FileNotFoundException异常。
* FileOutputStream(String name, boolean append) 
    创建一个向具有指定 name 的文件中写入数据的输出文件流
    * 构造方法每次执行会覆盖原文件中的数据，如果不希望覆盖数据，则将append设置为true。





# InputStream

## 描述

java.io.InputStream: 字节输入流顶层抽象父类，所有和字节相关的输入流都是它的子类。可以从目标中读取字节数据到程序中，包括本地文件或者网络。

## 成员方法

* abstract  int read()

​          从输入流中读取数据的下一个字节。 

* int read(byte[] b)

​          从输入流中读取一定数量的字节，并将其存储在缓冲区数组 b 中。 
* int read(byte[] b, int off, int len)

​          将输入流中最多 len 个数据字节读入 byte 数组。 

* void close()

​          关闭此输入流并释放与该流关联的所有系统资源。

* byte[] readAllBytes()

从输入流读取所有剩余字节。   

* long transferTo(OutputStream out)

从该输入流中读取所有字节，并按读取的顺序将字节写入给定的输出流。

 

# FileInputStream

## 描述

文件字节输入流，用于读取本地文件中的字节数据。

## 构造方法

* FileInputStream(File file) 
    通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的 File 对象 file 指定。 

* FileInputStream(String name) 
    通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的路径名 name 指定。 



注意事项：资源释放： 先开后关，后关先开







# 异常处理优化

## JDK7优化

~~~java
try(创建流对象语句；创建流对象语句...){//结束后自动关闭流对象
    //可能发生异常的代码
}catch(E e){
    //处理异常
}
~~~

## JDK9 优化

~~~java
Resource resource1 = new Resource(); 
Resource resource2 = new Resource(); 
//引入方式：直接引入 
try (resource1; resource2) { 
    //使用对象 
}//不常用，
~~~



# BufferedInputStream &BufferedOutputStream

## 描述

缓冲流：创建流对象时，会创建一个内种默认大小的缓冲区，把程序需要读写的数据保存在缓冲区，在读写数据时，不会与硬盘交互，改成与内存中的缓冲区中的数据交互，减少IO次数，提高读写效率

## 构造方法

* BufferedInputStream(InputStream in) 

    创建一个 BufferedInputStream并保存其参数，输入流 in供以后使用。  

* BufferedInputStream(InputStream in, int size) 

    创建具有指定缓冲区大小的 BufferedInputStream ，并保存其参数，输入流 in供以后使用。  

* BufferedOutputStream(OutputStream out) 

    创建一个新的缓冲输出流，以将数据写入指定的底层输出流。  

* BufferedOutputStream(OutputStream out, int size)

     创建一个新的缓冲输出流，以便以指定的缓冲区大小将数据写入指定的底层输出流。  





# Writer



## 描述

写入字符流的抽象类。



## 方法

* Writer append(char c) 
    将指定字符添加到此 writer。 
* Writer append(CharSequence csq) 
    将指定字符序列添加到此 writer。 
*  Writer append(CharSequence csq, int start, int end) 
    将指定字符序列的子序列添加到此 
* abstract  void close() 
    关闭此流，但要先刷新它。 
* abstract  void flush() 
    刷新该流的缓冲。 
* void write(char[] cbuf) 
     写入字符数组。 
* abstract  void write(char[] cbuf, int off, int len) 
    写入字符数组的某一部分。 
* void write(int c) 
    写入单个字符。 
* void write(String str) 
    写入字符串。 
*  void write(String str, int off, int len) 
              写入字符串的某一部分。 



# OutputStreamWriter

## 描述

字符流通向字节流的桥梁

## 构造方法

* OutputStreamWriter(OutputStream out) 
    创建使用默认字符编码的 OutputStreamWriter。 
* OutputStreamWriter(OutputStream out, Charset cs) 
    创建使用给定字符集的 OutputStreamWriter。 
* OutputStreamWriter(OutputStream out, CharsetEncoder enc) 
    创建使用给定字符集编码器的 OutputStreamWriter。 
* OutputStreamWriter(OutputStream out, String charsetName) 
    创建使用指定字符集的 OutputStreamWriter。 



## 方法

* void close() 
    关闭此流，但要先刷新它。 
* void flush() 
    刷新该流的缓冲。 
* String getEncoding() 
    返回此流使用的字符编码的名称。 
* void write(char[] cbuf, int off, int len) 
    写入字符数组的某一部分。 
* void write(int c) 
    写入单个字符。 
* void write(String str, int off, int len) 
    写入字符串的某一部分。 

***注意***：必须关流

# FileWriter

## 描述

用来写入字符文件的便捷类



##  构造方法

* FileWriter(File file) 
    根据给定的 File 对象构造一个 FileWriter 对象。 
* FileWriter(File file, boolean append) 
    根据给定的 File 对象构造一个 FileWriter 对象。 
* FileWriter(String fileName) 
    根据给定的文件名构造一个 FileWriter 对象。 
* FileWriter(String fileName, boolean append) 
    根据给定的文件名以及指示是否附加写入数据的 boolean 值来构造 FileWriter 对象。 



## 方法

都继承自父类



# Reader

## 描述

用于读取字符流的抽象类

## 方法

* abstract  void close() 
    关闭该流并释放与之关联的所有资源。 
* void mark(int readAheadLimit) 
    标记流中的当前位置。 
* boolean markSupported() 
    判断此流是否支持 mark() 操作。 
* int read() 
    读取单个字符。 
* int read(char[] cbuf) 
    将字符读入数组。 
* abstract  int read(char[] cbuf, int off, int len) 
    将字符读入数组的某一部分。 
* int read(CharBuffer target) 
    试图将字符读入指定的字符缓冲区。 
* boolean ready() 
    判断是否准备读取此流。 
* void reset() 
    重置该流。 
* long skip(long n) 
    跳过字符。 



# InputStreamReader

## 描述

字节流通向字符流的桥梁

## 构造方法

* InputStreamReader(InputStream in) 
    创建一个使用默认字符集的 InputStreamReader。 
* InputStreamReader(InputStream in, Charset cs) 
    创建使用给定字符集的 InputStreamReader。 
* InputStreamReader(InputStream in, CharsetDecoder dec) 
    创建使用给定字符集解码器的 InputStreamReader。 
* InputStreamReader(InputStream in, String charsetName) 
    创建使用指定字符集的 InputStreamReader。 

## 方法

* void close() 
    关闭该流并释放与之关联的所有资源。 
* String getEncoding() 
    返回此流使用的字符编码的名称。 
* int read() 
    读取单个字符。 
* int read(char[] cbuf, int offset, int length) 
    将字符读入数组中的某一部分。 
* boolean ready() 
    判断此流是否已经准备好用于读取。 

***注意***：必须关流

# FileReader

## 描述

用来读取字符文件的便捷类。

## 构造方法

* FileReader(File file) 
    在给定从中读取数据的 File 的情况下创建一个新 FileReader。 
* FileReader(FileDescriptor fd) 
    在给定从中读取数据的 FileDescriptor 的情况下创建一个新 FileReader。 
* FileReader(String fileName) 
    在给定从中读取数据的文件名的情况下创建一个新 FileReader。 

## 方法

继承自父类



# BufferredWriter&BufferredReader

* BufferredWriter
    * 特有方法void newLine•() 写一行行分隔符。  
* BufferredReader
    * 特有方法String readLine•() 读一行文字。







# Properties

## 描述

表示一组持久的属性。是一个特殊的map集合，

属性列表中的每个键和值都是字符串



## 构造方法

* Properties() 
    创建一个无默认值的空属性列表。 
* Properties(Properties defaults) 
    创建一个带有指定默认值的空属性列表。 



## 方法

* String getProperty(String key) 
              用指定的键在此属性列表中搜索属性。 
* String getProperty(String key, String defaultValue) 
              用指定的键在属性列表中搜索属性。 
* void list(PrintStream out) 
              将属性列表输出到指定的输出流。 
* void list(PrintWriter out) 
              将属性列表输出到指定的输出流。 
* void load(InputStream inStream) 
              从输入流中读取属性列表（键和元素对）。 
* void load(Reader reader) 
              按简单的面向行的格式从输入字符流中读取属性列表（键和元素对）。 
* Object setProperty(String key, String value) 
              调用 Hashtable 的方法 put。 
*  void store(OutputStream out, String comments) 
              以适合使用 load(InputStream) 方法加载到 Properties 表中的格式，将此 Properties 表中的属性列表（键和元素对）写入输出流。 
*  void store(Writer writer, String comments) 
              以适合使用 load(Reader) 方法的格式，将此 Properties 表中的属性列表（键和元素对）写入输出字符。 
* Set<String> stringPropertyNames() 
              返回此属性列表中的键集，其中该键及其对应值是字符串，如果在主属性列表中未找到同名的键，则还包括默认属性列表中不同的键。 

# ObjectOutputStream

## 描述

将Java对象通过输出流写到指定的文件中持久保存

是OutputStream的子类

## 构造方法

* ObjectOutputStream(OutputStream out)

创建一个ObjectOutputStream流，通过指定的OutputStream流写出对象。

## 成员方法

*  void writeObject(Object obj)

将指定的对象写入ObjectOutputStream。





# ObjectInputStream

## 描述

ObjectInputStream 对以前使用 ObjectOutputStream 写入的基本数据和对象进行反序列化。 



## 构造方法

* ObjectInputStream(InputStream in) 

创建从指定的InputStream读取的ObjectInputStream。  



## 成员方法

* Object readObject() 

从ObjectInputStream读取一个对象。 



# 序列化与反序列化注意事项

* 只有实现Serializable接口的类才能序列化或者反序列化

* 类实现了Serializable接口后，类中会产生一个串行版本号：

    ~~~java
    private static final long serialVersionUID = value；
    ~~~

    这个串行版本号的值是根据类中成员随机计算出的，当对象序列化后，会绑定这个串行版本号。

    反序列化对象时，会检测对象绑定的串行版本号与类中的是否一致，如果一致则通过序列化，否则报错

    为了避免报错可以手动为串行版本号赋值

* static 和 transient 修饰的成员变量，不会被序列化，反序列化时变量为默认值





# SequenceInputStream

## 描述

合并流就是将多个输入流合并为一个输入流，实现多个文件的一次读取。它从一个有序的输入流集合开始，从第一个读取到文件的结尾，然后从第二个文件读取，依此类推，直到最后一个输入流达到文件的结尾。

## 构造方法

* SequenceInputStream(Enumeration<? extends InputStream> e) 
    通过记住参数来初始化新创建的 SequenceInputStream，该参数必须是生成运行时类型为 InputStream 对象的 Enumeration 型参数。 

    * Enumeration对象可以通过Collections类的方法获取：

        ~~~java
        static <T> Enumeration<T> enumeration•(Collection<T> c)
        ~~~

        

* SequenceInputStream(InputStream s1, InputStream s2) 
    通过记住这两个参数来初始化新创建的 SequenceInputStream（将按顺序读取这两个参数，先读取 s1，然后读取 s2），以提供从此 SequenceInputStream 读取的字节。 



## 方法

* void close() 
    关闭此输入流并释放与此流关联的所有系统资源。 
* int read() 
    从此输入流中读取下一个数据字节。 
* int read(byte[] b, int off, int len) 
    将最多 len 个数据字节从此输入流读入 byte 数组。 





# 键盘录入

System类的成员变量in返回的是一个InputStream对象，可以通过该对象捕获键盘输入

通过System.in 实现键盘录入的模板

## 模板一

一次读取一个字节

~~~java
public static void main(String[] args) throws IOException {
    InputStream input = System.in;
    int ch;
    while ( (ch = input.read()) != -1 ) {
        if( ch == '0') {
            break;
        }
        System.out.println((char)ch);
    }
}
~~~

## 模板二

一次读取一行文本

~~~java
public static void main(String[] args) throws IOException {
    InputStream input = System.in;
    InputStreamReader isr = new InputStreamReader(input);
    BufferedReader br = new BufferedReader(isr);
    String line;
    while ( (line = br.readLine()) != null ) {
        // 约定读取到"over"结束程序
        if( line.equals("over")) {
            break;
        }
        System.out.println(line);
    }
}

~~~



# 打印流PrintStream

## 描述

提供控制台打印功能



## 构造方法

* PrintStream(File file) 
              创建具有指定文件且不带自动行刷新的新打印流。

* PrintStream(OutputStream out) 
              创建新的打印流。

* PrintStream(String fileName) 
              创建具有指定文件名称且不带自动行刷新的新打印流。



## 方法

* void print(Object obj) 
              打印对象。 

* void println(String x) 
              打印 String，然后终止该行。 



## 代码演示

~~~java
public static void main(String[] args) throws IOException {
    PrintStream ps = new PrintStream("d:\\demo\\ps.txt");
    // 更改打印的目标为文件中
    System.setOut(ps);

    ps.println("Hello World!");
    ps.println(97); 
    ps.write(97);
    ps.close();
}

~~~



# RandomAccessFile随机流

## 描述

* 提供文件读取和写入功能
* 为文件标记了下标
* 可以通过控制下标改变读写位置



## 构造方法

* RandomAccessFile(File file, String mode) 
* 创建一个随机访问文件流，从File参数指定的文件读取，并可选地写入。  
* RandomAccessFile(String name, String mode) 
* 创建随机访问文件流，以从中指定名称的文件读取，并可选择写入文件。  

参数mode ： r: 只读     rw： 读写



## 方法

* void seek(long pos)

 设置文件指针偏移，从该文件的开头测量，发生下一次读取或写入。  
