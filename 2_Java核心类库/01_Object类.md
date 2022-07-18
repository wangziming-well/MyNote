## toString

~~~java
String toString(); 返回该对象的字符串表示
~~~

得到对象的属性信息

实例化对象后，直接调用对象名，会隐式默认调用Object类中的toString方法;

~~~java
class Person{
    
}
Person p = new Person();
System.out.println(p);
System.out.println(p.toStirng());
~~~

以上代码5,6行是等价的；

会返回对象的地址信息，在实际开发中，得到地址信息对程序员没有任何意义，我们更加想要得到的是对象的属性内容信息，所以我们需要在子类重写Object 的toString方法；



## equals方法

~~~java
boolean equals(Object obj) //:指使其他某个对线是否与此对象"相等"
~~~



Object中的equals方法比较的两个对象的地址值，实际运用中，根据需要重写；

