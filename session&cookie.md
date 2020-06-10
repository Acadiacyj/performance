# session&cookie&application
cookie通过在客户端记录信息确定用户身份，Session通过在服务器端记录信息确定用户身份。

cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session。

session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie。

单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

可以考虑将登陆信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中。
## session
### 定义
当访问服务器否个网页的时候，会在服务器端的内存里开辟一块内存，这块内存就叫做session，而这个内存是跟浏览器关联在一起的。这个浏览器指的是浏览器窗口，或者是浏览器的子窗口，意思就是，只允许当前这个session对应的浏览器访问，就算是在同一个机器上新启的浏览器也是无法访问的。而另外一个浏览器也需要记录session的话，就会再启一个属于自己的session

### 原理
HTTP协议是非连接性的，当关闭浏览器，链接断开后没有方法获取信息。那么需要获取到对应的浏览器session信息则通过生成的唯一sessionid

### 数据传递方法









参考文献：
1.https://www.cnblogs.com/8023-CHD/p/11067141.html

2.https://blog.csdn.net/weixin_42217767/article/details/92760353
