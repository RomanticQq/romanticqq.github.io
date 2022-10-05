---
title: Ajax原理和使用
tags:
  - 前端
categories: 前端
abbrlink: 35823
date: 2021-01-15 12:26:31
---
1. #### http介绍
&nbsp;&nbsp;&nbsp;&nbsp;HTTP基于TCP,是面向连接的协议，建立需要通过**三次握手**，断开需要通过**四次挥手**。
&nbsp;&nbsp;&nbsp;&nbsp;当连接断开时，客户端的**最后一次挥手**后会等待两个单位时间，若两个单位时间内没有收到任何响应，说明服务器关闭了，然后客户端也关闭；若两个单位时间内又收到了消息，说明服务器还没有关，客户端和服务端将继续沟通。
![](https://myforpicgo.oss-cn-beijing.aliyuncs.com/image/20210115125141.PNG)

2. #### http协议的构成
**请求**：
+ 请求头--request header
    + URL
    + method
    + query
+ 请求体--request body
**响应**：
+ 响应头--request header
    + content-type
+ 响应体--response body
    + 响应数据

当是`get`请求时,信息在`URL`中；当是`post`请求时，信息在`request body`中。
`content-type`中表示返回的数据类型，返回的数据在`response body `中。

3. #### 同步和异步
&nbsp;&nbsp;&nbsp;&nbsp;同步:代码按照前后顺序一行一行的执行；
&nbsp;&nbsp;&nbsp;&nbsp;异步：同时执行多行代码；
&nbsp;&nbsp;&nbsp;&nbsp;注：异步代码总是在同步代码之后执行；

&nbsp;&nbsp;&nbsp;&nbsp;现在的前后端交互采取前后端分离，我们会采用异步的JavaScript和XML或JSON格式来完成数据的局部刷新。因为它是异步的，所以不等待整需要个页面的刷新，只需要发送一个异步请求，什么时候请求的内容过来了，什么时候刷新局部页面

4. #### Ajax介绍
&nbsp;&nbsp;&nbsp;&nbsp;传统的项目前后端不分离，用户触发一个http请求服务器，然后服务器收到之后再做出响应给用户，并且返回一个新的页面，也就是说交互都是通过页面刷新或页面跳转来实现的。

&nbsp;&nbsp;&nbsp;&nbsp;这种方式对于用户体验来讲其实并不友好，少量的数据更新也会引发整个页面重新请求，浪费了很大一部分资源。

&nbsp;&nbsp;&nbsp;&nbsp;因此，我们希望有一种更好的方式，可以不用重新请求整个页面而达到更新部分数据的效果。*2005年，ajax(Asynchronous JavaScript And XML)出现，给前端带来了巨大的变化与革新。*

5. #### Ajax的特点
优点：
+ 不需要插件支持（一般浏览器且默认开启JavaScript即可）
+ 用户体验极佳（不刷新页面即可获取可更新的数据）
+ 提升Web程序的性能（在传递数据方面做到按需发送，不必整体提交）
+ 减轻服务器和带宽的负担（将服务区的一些操作转移到客户端）

缺点：
+ 前进、后退功能被破坏（因为Ajax永远在当前页面，不会记录前后页面）
+ 搜索引擎的支持度不够（因为搜索引擎爬虫还不能理解JS引起变化数据的内容）
  
6. #### 常见状态码
+ 100-199：表示连接继续
+ 200-299：表示各种意义上的成功
+ 300-399：表示重定向
+ 400-499：表示各种客户端错误
+ 500-599：表示各种服务端错误

7. #### Ajax原理
&nbsp;&nbsp;&nbsp;&nbsp;1.准备页面请求，创建XMLHttpRequest对象
&nbsp;&nbsp;&nbsp;&nbsp;2.使用XMLHttpRequest对象的open()和send()方法发送资源请求给服务器
&nbsp;&nbsp;&nbsp;&nbsp;3.后台计算
&nbsp;&nbsp;&nbsp;&nbsp;4.onreadystatechange函数，状态改变时发送数据回客户端，使用XMLHttpRequest对象的responseText或responseXML属性获得服务器的响应

&nbsp;&nbsp;&nbsp;&nbsp;注：open()打开连接，send()向服务器发送资源;调用send()方法后要去监听onreadystatechange事件，当onreadystatechange状态改变时，说明后端发送数据给客户端，客户端接收数据。

8. #### Ajax(get)
具体流程看注释

client代码：
```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<button onclick="sendMsg()">发送请求</button>
	<div id="id1"></div>
	<script type="text/javascript">
		function sendMsg(){
			// 1.创建一个XMLHttpRequest对象
			var xhr=new XMLHttpRequest();
			// 2.调用open方法打开连接
			// open方法有三个参数
			// 1.请求的method
			// 2.请求的url
			// 3.是否异步，默认值为true
			xhr.open('get','http://127.0.0.1/data.php?id=1');
			//3.发送请求
			xhr.send();
			//4.监听状态的改变
			xhr.onreadystatechange=function (){
				// 判断状态值 0-4 五种状态，4代表最终的完成
				if(xhr.readyState === 4){
					// 判断状态码
					if(xhr.status === 200){
						//将返回的字符串转换成json对象
						var resp=JSON.parse(xhr.responseText);
						console.log(resp);
						document.querySelector('div').innerHTML=`
						<h2>编号：${resp.id}</h2>
						<h2>标题：${resp.title}</h2>`		
					}
				}
			}
		}
	</script>
</body>
</html>
```
server代码：
```php
<?php
// 解决跨域问题
header("Access-Control-Allow-Origin:*");
header('Access-Control-Allow-Methods:POST');
header('Access-Control-Allow-Headers:x-requested-with, content-type');
//获取客户端get请求过来的数据
$id=$_GET['id'];
//转换成json格式
echo json_encode(array('id'=>$id,'title'=>'Hello Ajax'));
```

8. #### Ajax(post)
get请求和post请求有很多地方都相同，注意不同的地方(注释处)
client代码
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<button onclick="sendMsg()">发送请求</button>
<div id="id1"></div>
<script type="text/javascript">
    function sendMsg(){
        var xhr=new XMLHttpRequest();
        // method为post
        xhr.open('post','http://127.0.0.1/data.php');
        //设置请求头的content-type  指定了参数的发送方式
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
        // 在send里写需要发送的数据
        xhr.send('name=zhangsan&age=18');
        xhr.onreadystatechange=function (){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var resp=JSON.parse(xhr.responseText);
                    console.log(resp);
                    document.querySelector('div').innerHTML=`
						<h2>姓名：${resp.name}</h2>
						<h2>年龄：${resp.age}</h2>`
                }
            }
        }
    }
</script>
</body>
</html>
```
server代码：
```php
<?php
// 解决跨域问题
header("Access-Control-Allow-Origin:*");
header('Access-Control-Allow-Methods:POST');
header('Access-Control-Allow-Headers:x-requested-with, content-type');
//获取客户端get请求过来的数据
$name=$_POST['name'];
$age=$_POST['age'];
//转换成json格式
echo json_encode(array('name'=>$name,'age'=>$age));
```

9. #### 封装ajax(1)
get封装：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<button onclick="sendMsg()">发送请求</button>
<script type="text/javascript">
    function sendMsg(){
        //若无参数query为null
        //若有参数，{}
        get('http://127.0.0.1/data.php',{name:'xiaoming',age:18},function(resp){
            console.log(resp)
        },true)
    }
    //封装get请求
    //query： string,请求的地址
    //query： Object,请求携带的参数
    //callback: function,成功之后的回调
    //isJSON: boolean,是否转化为json格式
    function get(url,query,callback,isJSON){
        //若有参数,先把参数拼接在url后面
        if(query){
            url+='?'
            for(var key in query){
                url+=`${key}=${query[key]}&`
            }
            //取出最后多余的&
            url=url.slice(0,-1)
        }
        var xhr=new XMLHttpRequest()
        xhr.open('get',url)
        xhr.send()
        xhr.onreadystatechange=function(){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var res=isJSON?JSON.parse(xhr.responseText):xhr.responseText
                    callback(res)
                }
            }
        }
    }
</script>
</body>
</html>
```

post封装
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<button onclick="sendMsg()">发送请求</button>
<script type="text/javascript">
    function sendMsg(){
        //若无参数query为null
        //若有参数，{}
        post('http://127.0.0.1/data.php',{'name':'xiaoming','age':18},function(resp){
            console.log(resp)
        },true)
    }
    //封装post请求
    //query： string,请求的地址
    //query： Object,请求携带的参数
    //callback: function,成功之后的回调
    //isJSON: boolean,是否转化为json格式
    function post(url,query,callback,isJSON){
        //若有参数,先把参数拼接起来
        var str=''
        if(query){
            for(var key in query){
                str+=`${key}=${query[key]}&`
            }
            //取出最后多余的&
            str=str.slice(0,-1)
        }
        var xhr=new XMLHttpRequest()
        xhr.open('post',url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(str)
        xhr.onreadystatechange=function(){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var res=isJSON?JSON.parse(xhr.responseText):xhr.responseText
                    callback(res)
                }
            }
        }
    }
</script>
</body>
</html>
```
**注**：测试时一定要注意，当前端发的方式和后端接受的方式不一样时，可能会报json格式错误

10.  #### ajax封装(2)
创建util.js
```js
//创建一个util对象，切记对象内的数据之间要有逗号隔开
var util={
    //封装get
    get:function (url,query,callback,isJSON){
        //若有参数,先把参数拼接起来
        var str=''
        if(query){
            for(var key in query){
                str+=`${key}=${query[key]}&`
            }
            //取出最后多余的&
            str=str.slice(0,-1)
        }
        var xhr=new XMLHttpRequest()
        xhr.open('post',url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(str)
        xhr.onreadystatechange=function(){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var res=isJSON?JSON.parse(xhr.responseText):xhr.responseText
                    callback(res)
                }
            }
        }
    },

    //封装post
    post:function (url,query,callback,isJSON){
        //若有参数,先把参数拼接起来
        var str=''
        if(query){
            for(var key in query){
                str+=`${key}=${query[key]}&`
            }
            //取出最后多余的&
            str=str.slice(0,-1)
        }
        var xhr=new XMLHttpRequest()
        xhr.open('get',url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(str)
        xhr.onreadystatechange=function(){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var res=isJSON?JSON.parse(xhr.responseText):xhr.responseText
                    callback(res)
                }
            }
        }
    }
}

//调用时
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<button onclick="sendMsg()">发送请求</button>
//先引入js文件,然后调用即可
<script src="./util.js"></script>
<script type="text/javascript">
    function sendMsg(){
        //若无参数query为null
        //若有参数，{}
        util.post('http://127.0.0.1/data.php',{'name':'xiaoming','age':18},function(resp){
            console.log(resp)
        },true)
    }
</script>
</body>
</html>
```
11. #### ajax封装(3)
server代码：
```JavaScript
var util={
    //param : Object{method,url,query,callback,isJSON}
    ajax:function(params){
        var xhr=new XMLHttpRequest()
        if(params.method === 'get'){
            params.url+='?'
            for(var key in params.query){
                params.url+=`${key}=${params.query[key]}&`
            }
            params.url=params.url.slice(0,-1)
            xhr.open('get',params.url)
            xhr.send()
        }else{
            var str=''
        if(params.query){
            for(var key in params.query){
                str+=`${key}=${params.query[key]}&`
            }
            //取出最后多余的&
            str=str.slice(0,-1)
        }
        var xhr=new XMLHttpRequest()
        xhr.open('post',params.url)
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        xhr.send(str)
        }
        xhr.onreadystatechange=function(){
            if(xhr.readyState === 4){
                if(xhr.status === 200){
                    var resp=params.isJSON ? JSON.parse(xhr.responseText) : xhr.responseText
                    params.callback(resp)
                }
            }
        }
    }
}
```
client代码
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<button onclick="sendMsg()">发送请求</button>
<script src="./util.js"></script>
<script type="text/javascript">
    function sendMsg(){
        util.ajax({
        	method:'get',
        	isJSON:true,
        	url:'http://127.0.0.1/data.php',
        	query:{
        		'name':'xiaoming',
        		'age':18
        	},
        	callback:function(resp){
                console.log(resp)
        	}
        })   
    }
</script>
</body>
</html>
```
