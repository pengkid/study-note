

## AJAX（异步的javascript和xml）{#index1}

在不重新加载（刷新）页面的情况下，客户端和服务器端进行小量的数据交互，从而对页面某块区域的结构和样式进行更新。


异步的特点：

当你填写一个表单时，客户端会同时把填写的数据传给服务器并验证（避免了提交后才进行数据传输验证而导致的时间等待）

并且由于是实时验证，如果数据有问题，服务端能立刻报错，并通过在客户端改变样式（变红或文字）来提示用户的数据有问题（解决了重新填写的问题）

意味着 客户端和服务端 互相之间的操作不会发生堵塞


## XMLHttpRequest{#index2}

```
兼容所有浏览器，创建XHR对象

var option = {
    url: ,
    data:{
    	//
    },
    dataType: "json",
    method: GET || POST,
    success: function(res){},
    fail: function(res){}
} || {}

if(window.XMLHttpRequest) var request = new XMLHttpRequest();
else var request = new ActiveXObject();

.onreadystatechange = function () {
    if (xhr.readyState == 4) {
	var status = xhr.status;
	if (status >= 200 && status < 300) {
		options.success && options.success(xhr.responseText, xhr.responseXML);
      } 
	else {
                            options.fail && options.fail(status);
                        }
                    }
                }

```
	HTTP请求

		HTTP是计算机网络通信的一种协议，它是无状态协议（客户端请求，服务端应答）

		一个完整的HTTP请求过程（客户端请求，服务端应答）共有七个步骤：

			1.与服务器端建立TCP/IP连接

			2.Web浏览器向Web服务器发送请求命令

			3.Web浏览器发送请求头信息

			4.Web服务器应答

			5.Web服务器发送应答头信息

			6.Web服务器向浏览器发送数据

			7.Web服务器关闭TCP/IP连接



		一个HTTP请求（客户端请求）一般由四部分组成

			1.HTTP请求的方法或动作，如 GET or POST

				GET：	一般用于信息获取

					使用URL传递参数，因此信息对用户是可见的

					发送的信息有数量限制


				POST：	一般用于修改服务器上的资源

					信息嵌入HTTP请求体里，因此信息对用户是不可见的

					发送信息无数量限制


			2.正在请求的URL，即要访问的地址

			3.请求头，包含一些客户端环境信息，身份验证信息

			4.请求体，也就是请求正文，请求正文中可以包含客户提交的查询字符串信息，表单信息等



		一个HTTP响应（服务端应答）一般由三部分组成

			1.一个数字和文字组成的状态码，用来显示请求是成功还是失败

			2.响应头，响应头也和请求头一样包含许多有用的信息，如服务器类型，日期时间，内容类型和长度等

			3.响应体，也就是响应正文（字符串，HTML代码等）



		HTTP状态码由3位数字构成

			1XX：信息类，表示服务器收到了浏览器的请求 并正在处理

			2XX：成功，表示客户端请求被服务器正确接收和处理，如：200 OK

			3XX：重定向，表示请求没成功，客户必须采取进一步动作

			4XX：客户端错误，表示客户端请求有错误，如：404 NOT Found，意味着请求中引用的文档不存在

			5XX：服务器错误，表示服务器不能完成对请求的处理，如：500


