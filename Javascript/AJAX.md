

## AJAX（异步的javascript和xml）

在不重新加载（刷新）页面的情况下，客户端和服务器端进行小量的数据交互，从而对页面某块区域的结构和样式进行更新。


## XMLHttpRequest对象

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

