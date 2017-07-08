## localStorage与sessionStorage

### 两个共有的接口：

* getItem(key):获取指定key本地存储的值。

* setItem(key,value):将value存储到key字段。

* removeItem(key):删除指定key本地存储的值。

* lenth:存储的项目数。

* clear():会清除所有数据。

### sessionStorage与 localStorage 的异同

sessionStorage会在关闭浏览器后删除数据，在chrome51版本下，关闭同一域名下的所有页面也会删除数据。

localStorage是一个持久化的存储，它并不局限于会话。