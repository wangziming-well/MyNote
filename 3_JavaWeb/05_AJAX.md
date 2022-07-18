# AJAX介绍

Asynchronized Javascript And XML 技术，异步刷新技术

可以实现页面的局部位置刷新，而不需要跳转页面



# XMLHttpRequest

JS内置了XMLHttpRequest对象，封装了异步请求的功能

JS内置对象XMLHttpRequest()来实现页面的

## 方法

方法实现了发送请求功能

* `open(method,url,async)`

    规定异步请求的类型，URL以及是否异步

    * method:请求的类型“get”或“post”
    * url:请求的资源路径
    * async:异步true或false

* `send(string)`

    发送请求，string：仅用于PSOT请求

## 属性 

属性实现了等待响应功能

* `onreadstatechange`

    存储函数，当readyState属性改变时，会调用该函数

* `readState`

    响应码

    表示XMLHttpRequest的响应状态

    * 0：请求初始化
    * 1：服务器连接已建立
    * 2：请求已接收
    * 3：请求处理中
    * 4：请求完成，响应就绪

* `status`

    状态码

    200：“OK”

    404：未找到页面

* `responseText`

    字符串形式的响应数据

## 模板

以get请求为例

~~~js
//发送请求
var xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("get","reqeustDemo.action",true);
xmlHttpReqesut.send();

//接受请求
xmlHttpRequest.onreadystatechange= function(){
    //当状态码为4时且服务器响应成功时，接受响应信息
    if(xmlHttpRequest.readState ==4 && xmlHttpRequest.status == 200 ){
        var response = xmlHttpRequest.responseText;
        alert(response)
    }
}
~~~



# jQuery封装的AJAX

jQuery对XMLHttpRequest对象进行了进一步的封装

## $.ajax

$.ajax([settings]) 的参数是json对象，通过json的字段与值控制异步请求与响应

json参数常用字段：

* `type`

    请求方式

    * “get”
    * "post"

* `url`

    请求资源路径

* `async`

    是否异步

    * true（默认）
    * false

* `cache`

    是否在浏览器产生缓存

    * true（默认）
    * false

* `contextType`

    发送信息到服务器时内容的编码类型

    * "application/x-www-form-urlencoded"(默认)

* `data`

    发送给服务器的数据

    (如果data是字符串需以 “键=值&键=值”的形式传递)

* `dataType`

    服务器响应值的预期数据类型，ajax会按照该字段处理响应字符串

    * text（默认）
    * xml
    * json

* `enctype`

    编码格式

    * “”（默认）
    * "multipart/form-data"上传文件时

* `success`响应成功时的回调函数

* `error`响应失败时的回调函数

## \$.get & \$.post

`$.get(url[,data,success(response[,status,xhr]),dataType])`

简单的get异步请求

* success(response,status,xhr)	
    当请求成功时运行的函数。额外的参数：
    * response - 包含来自请求的结果数据
    * status - 包含请求的状态
    * xhr - 包含 XMLHttpRequest 对象

`$.post(url[,data,success(data[, textStatus, jqXHR]),dataType])`

简单的post异步请求，参数同上

**注意：**如果在用\$.get和\$.post想控制其他字段可以用

`$.ajaxSettings`获取或设置ajax配置，相当于获取jQuery.ajax(url,[settings])方法中的settings。