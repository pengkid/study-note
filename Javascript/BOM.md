* [概述](#index1)
* [窗口](#index2)
* [Navigator](#index3)
* [BOM](#index4)
  * [window下的全局变量](#index4.1)

## <font color="4590a3">概述{#index1}</font>

javascript所有对象都在`window`这个**顶层对象**之中。

```
var a = 1;

window.a  // 1
```

> 所有未声明就赋值的变量都自动变成window对象的属性。

## <font color="4590a3">窗口{#index2}</font>

* window.screenX，window.screenY

返回浏览器窗口左上角相对于当前屏幕左上角（\(0, 0\)）的水平距离和垂直距离，单位为像素。

* window.innerHeight，window.innerWidth

返回网页在当前窗口中可见部分的高度和宽度，即“视口”（viewport），单位为像素。

* window.outerHeight，window.outerWidth

返回浏览器窗口的高度和宽度，包括浏览器菜单和边框，单位为像素。

* window.pageXOffset属性，window.pageYOffset属性

window.pageXOffset属性返回页面的水平滚动距离，window.pageYOffset属性返回页面的垂直滚动距离，单位都为像素。

* screen.height、screen.width

`screen.availHeight`和`screen.availWidth`属性返回屏幕可用的高度和宽度，单位为像素。它们的值为屏幕的实际大小减去操作系统某些功能占据的空间，比如系统的任务栏。

`screen.colorDepth`属性返回屏幕的颜色深度，一般为16（表示16-bit）或24（表示24-bit）。

## <font color="4590a3">navigator对象{#index3}</font>

* navigator.userAgent属性

返回浏览器的User-Agent字符串，用来标示浏览器的种类。

我目前浏览器信息：

> "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36"



## <font color="4590a3">BOM{#index4}</font>

window 也是 BOM 的一个对象，除去编程意义上的“兜底对象”之外，通过这个对象可以获取窗口位置、确定窗口大小、弹出对话框等等。例如我要关闭当前窗口：

```
window.close();

```

DOM 是为了操作文档出现的 API，document 是其的一个对象；

BOM 是为了操作浏览器出现的 API，window 是其的一个对象。


### <font color="4590a3">window下的全局变量{#index4.1}</font>

* `innerHeight/innerWidth`：浏览器窗口内部高度/宽度

* `navigator`：包含有关访问者浏览器的信息

* `screen`：访问者屏幕的宽度，以像素计

* `setTimeout()/clearTimeout()`：定时器/取消定时

* `document.cookie`：现在多数网站使用Cookie来识别用户

* `window.location`:对象用于访问当前 URL，或者导航到新的页面

  * `hostname` ：web 主机的域名
  * `pathname` ：当前页面的路径和文件名
  * `port` ：web 主机的端口
  * `protocol` ：所使用的 web 协议（http:// 或 https://）
  * `href` ：当前url，对它赋值可以实现重定向
  * `reload()` ：这是一个方法，调用后会刷新当前页面
  

* `window.history`:提供浏览器历史的操作

  * `history.back()` ：与在浏览器点击后退按钮相同
  * `history.forward()` ：与在浏览器中点击按钮向前相同
  * `history.go(num)` ：num可正可负，正则前进，负则后退



