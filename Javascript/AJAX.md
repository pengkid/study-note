  
## 概述

AJAX（异步的javascript和xml）

在不重新加载（刷新）页面的情况下，客户端和服务器端进行小量的数据交互，从而对页面某块区域的结构和样式进行更新。


## 完整的 AJAX 请求

### 新建XMLHttpRequest对象

```js
//创建通信对象
var request;

//兼容性问题
if(window.XMLHttpRequest){
    request = new XMLHttpRequest();
}
else {
    request = new ActiveXObject('Microsoft.XMLHTTP');
}

//配置常量
const options = {
    url: ,                       //请求地址
    data:{ },                    //请求数据 
    dataType: "json",            //数据类型
    method: GET || POST,         //请求方法
    success: function(res){//代码},    //成功函数
    fail: function(res){//代码}        //失败函数
} || {}

```

### 新建服务器

#### get请求
```js
request.open('get', url [, boolean]);  //比喻：在地址栏输入地址
request.send();  //提交请求，比喻：按了一下回车

```
##### 参数
* `method` : 请求方法，get请求则为 "get"
* `url` : 请求地址，请求参数写在`?`后面，如果URL含有中文，会出现乱码，要使用`encodeURI`编码URL
* `boolean` ： 是否异步请求，默认是 false

#### post请求
```js
xhr.open('post', url [, boolean]);
xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');  //申明发送的数据类型，post没有缓存问题，无需编码
xhr.send('username=pengkid&age=18'); //请求参数写在send方法中
```
##### 参数
* `method` : 请求方法，post请求则为 "post"
* `url` : 请求地址，无须写请求参数
* `boolean` ： 是否异步请求，默认是 false


### 等待服务器返回内容

#### 监听通信对象的状态码
```js
request.onreadystatechange = function () {
    if (request.readyState == 4) {
        var status = request.status;
	if (status >= 200 && status < 300) {
	    options.success && options.success(request.responseText);
	} 
	else options.fail && options.fail(status);
    }
}
```

#### readyState取值

0：请求未初始化（还没有调用 open()）。
1：请求已经建立，但是还没有发送（还没有调用 send()）。
2：请求已发送，正在处理中（通常现在可以从响应中获取内容头）。
3：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。
4：请求完毕且响应已完成；您可以获取并使用服务器的响应了。
从发送请求到对后端的返回的数据进行处理的状态值变化。 但如果没有相应的文件，也有错误信息返回，这是状态值也是一样，所有还需要加入status。

#### status服务器状态

`status == 200 //服务器响应成功 `

`request.responseText //服务器响应数据`

返回的是json字符串，可以用JSON.parse()把字符串转换为json对象。


## Jquery 的 AJAX封装

```js
$.ajax({
    url:'',
    type:'POST', //GET
    async:true,    //或false,是否异步
    data:{
        name:'pengkid',
        age:18
    },
    timeout:5000,    //超时时间
    dataType:'json',    //返回的数据格式：json/xml/html/script/jsonp/text
    beforeSend:function(xhr){
        console.log(xhr);
        console.log('发送前');
    },
    success:function(data,textStatus,jqXHR){
        console.log(data);
        console.log(textStatus);
        console.log(jqXHR);
    },
    error:function(xhr,textStatus){
        console.log('错误');
        console.log(xhr);
        console.log(textStatus);
    },
    complete:function(){
        console.log('结束');
    }
})
```


