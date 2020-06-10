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
1.将sessionId放入临时cookie中

2.通过response.encodeURL()方法进行URL重写，URL后面加入sessionID，当不支持cookie的时候，可以使用encodeURL()方法，encodeUTL()后面跟上sessionID，这样的话，在禁用cookie的浏览器中同时也可以使用session了

### 注意点
浏览器支持cookie，创建session时，将sessionID保存在cookie里。只要浏览器允许cookie，session就不会改变，如果不允许使用cookie，每刷新一次浏览器就会换一个session（因为浏览器以为这是一个新的链接）

Session不像cookie一样拥有路径访问的问题，同一个application下的servlet/jsp都可以共享同一个session，前提下是同一个客户端窗口。

session用于是string类

session理论上可以存放任何数据

### 常用方法
isNew()：是否是新的Session，一般在第一次访问的时候出现

getid()：拿到session，获取ID

getCreationTime()：当前session创建的时间

getLastAccessedTime()：最近的一次访问这个session的时间。

getRrquestedSessionid： 跟随上个网页cookies或者URL传过来的session

isRequestedSessionIdFromCookie()：是否通过Cookies传过来的

isRequestedSessionIdFromURL()：是否通过重写URL传过来的

isRequestedSessionIdValid()：是不是有效的sessionID

### 有限期限

当浏览器的某窗口关闭后关闭后不会立即清除session，而是有一个时间间隔(可设置)，当超过这个时间间隔则清除session，而在此间隔内访问这个sessionid则重新计时。

## cookie


参考文献：
1.https://www.cnblogs.com/8023-CHD/p/11067141.html

2.https://blog.csdn.net/weixin_42217767/article/details/92760353
