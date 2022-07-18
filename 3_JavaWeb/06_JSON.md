# JSON简介

* JSON 指的是 JavaScript 对象标记法（JavaScript Object Notation）
* JSON 是一种轻量级的数据交换格式
* JSON 具有自我描述性且易于理解
* JSON 独立于语言*

* JSON 使用 JavaScript 语法，但是 JSON 格式是纯文本的。文本可被任何编程语言作为数据来读取和使用。



# JSON格式

在js中

* {}表示JSON对象
* json数据由键值对组成，键和值中间用`:`隔开，键值对与键值对之间由`,`隔开
* json键只能是字符串
* json值可以是几乎任何对象（字符串，数字，json对象，数组，null，其他对象）

示例：

~~~js
var JSONDemo ={
    "name" :"alice",
    "age" : 19,
    "birth" : new Date(2018, 11, 24, 10, 33, 30, 0),
    "family":{
        "mother":"",
        "father":"",
        "sister":"",
        "brother":""
    },
    "hobby":["吃","睡"]
}
~~~

# JS中的JSON对象

* 创建JSON对象

    用`{}`

* 获取值：

    * `JSONDemo.name`
    * `JSONDemo["name"]`

* 添加/修改值：

    `JSONDemo["name"] = "Tom"`

* 删除值：

    `delete JSONDemo.name`

# JS中的JSON工具类

js中内置了JSON对象的工具类，提供了一些静态方法

* `JSON.parse(string)`

    解析字符串文本，返回一个json对象

    同样可以解析数组，返回json数组

* `JSON.stringify(json)`

    将json对象转换为字符串文本



# Java中的JSON

可以通过各种第三方包解析，生成json

## JsonUtil类

maven依赖：

~~~xml
<!--需要手动导包，maven的中央仓库中没有 -->
<dependency>
    <groupId>net.sf.json-lib</groupId>
    <artifactId>json-lib</artifactId>
    <version>2.4</version>
    <classifier>JDK16</classifier>
</dependency>
~~~

* `static String fromObject(Object object)`

    可以将Object类序列化为JSON字符串文本

## Gson类

maven依赖:

~~~xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.2</version>
</dependency>
~~~

* `String toJson(Object object) `

    将Object序列化为JSON字符串文本

