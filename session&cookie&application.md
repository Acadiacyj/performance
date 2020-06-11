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
由于HTTP协议是无状态的，而服务器端的业务必须是要有状态的。Cookie诞生的最初目的是为了存储web中的状态信息，以方便服务器端使用。它保存在客户端，当我们使用自己的电脑通过浏览器进行访问网页的时候，服务器就会生成一个证书并返回给我的浏览器并写入我们的本地电脑。这个证书就是cookie。一般来说cookie都是服务器端写入客户端的纯文本文件。Cookie 必须有浏览器的支持，在浏览器中设置阻止cookie，那么服务器端就不能写入cookie 到客户端了。大多数浏览器都支持cookie。

### 运作流程
（1）客户端在浏览器的地址栏中键入Web服务器的URL，浏览器发送读取网页的请求。

（2）服务器接收到请求后，产生一个Set-Cookie报头，放在HTTP报文中一起回传客户端，发起一次会话。

（3）客户端收到应答后，若要继续该次会话，则将Set-Cook-ie中的内容取出，形成一个Cookie.txt文件储存在客户端计算机里。

（4）当客户端再次向服务器发出请求时，浏览器先在电脑里寻找对应该网站的Cookie.txt文件。如果找到，则根据此Cookie.txt产生Cookie报头，放在HTTP请求报文中发给服务器。

（5）服务器接收到包含Cookie报头的请求，检索其Cookie中与用户有关的信息，生成一个客户端所请示的页面应答传递给客户端。 浏览器的每一次网页请求，都可以传递已存在的Cookie文件，例如，浏览器的打开或刷新网页操作。

### 属性
服务器端像客户端发送Cookie是通过HTTP响应报文实现的，在Set-Cookie中设置需要像客户端发送的cookie，例：Set-Cookie: "name=？;domain=？;path=？;expires=？;HttpOnly;secure"，其中name=value是必选项。

name:一个唯一确定的cookie名称。通常来讲cookie的名称是不区分大小写的


value:存储在cookie中的字符串值。最好为cookie的name和value进行url编码
domain:cookie对于哪个域是有效的。所有向该域发送的请求中都会包含这个cookie信息。这个值可以包含子域(如：yq.aliyun.com)，也可以不包含它(如：.aliyun.com，则对于aliyun.com的所有子域都有效)

path: 表示这个cookie影响到的路径，浏览器跟会根据这项配置，像指定域中匹配的路径发送cookie

expires:失效时间，表示cookie何时应该被删除的时间戳(也就是，何时应该停止向服务器发送这个cookie)。如果不设置这个时间戳，浏览器会在页面关闭时即将删除所有cookie；不过也可以自己设置删除时间。这个值是GMT时间格式，如果客户端和服务器端时间不一致，使用expires就会存在偏差

max-age: 与expires作用相同，用来告诉浏览器此cookie多久过期（单位是秒），而不是一个固定的时间点。正常情况下，max-age的优先级高于expires

HttpOnly: 告知浏览器不允许通过脚本document.cookie去更改这个值，同样这个值在document.cookie中也不可见。但在http请求张仍然会携带这个cookie。注意这个值虽然在脚本中不可获取，但仍然在浏览器安装目录中以文件形式存在。这项设置通常在服务器端设置

secure: 安全标志，指定后，只有在使用SSL链接时候才能发送到服务器，如果是http链接则不会传递该信息。就算设置了secure 属性也并不代表他人不能看到你机器本地保存的 cookie 信息，所以不要把重要信息放cookie就对了服务器端设置

### 要点
如果给cookie设置一个过去的时间，浏览器会立即删除该cookie

domain项必须有两个点，因此不能设置为localhost:

## application



参考文献：

1.https://www.cnblogs.com/8023-CHD/p/11067141.html

2.https://blog.csdn.net/weixin_42217767/article/details/92760353

3.https://blog.csdn.net/zhangquan_zone/article/details/77627899

4.https://blog.csdn.net/u014753892/article/details/52821268?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase

5.https://blog.csdn.net/echojson/article/details/79701795
