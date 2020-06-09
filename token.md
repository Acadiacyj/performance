# token

Token是服务端生成的一串字符串，以作客户端进行请求的一个令牌，当第一次登录后，服务器生成一个Token便将此Token返回给客户端，以后客户端只需带上这个Token前来请求数据即可，无需再次带上用户名和密码。

## 为什么用token

1.Token是在客户端频繁向服务端请求数据，服务端频繁的去数据库查询用户名和密码并进行对比，判断用户名和密码正确与否，并作出相应提示，在这样的背景下，Token便应运而生，即token是为了减轻服务器的压力，减少频繁的查询数据库，使服务器更加健壮。
2.Token 完全由应用管理，所以它可以避开同源策略。
3.Token 可以避免 CSRF 攻击。
4.Token 可以是无状态的，可以在多个服务间共享。

## 常用的token

1.用设备号/设备mac地址作为Token
2.用session值作为Token
3.后端生成

## token的运行流程

1.客户端使用用户名跟密码请求登录（或者带上设备mac地址/sessionid作为token）
2.服务端收到请求，去验证用户名与密码
3.验证成功后，服务端会签发一个 Token，再把这个 Token 发送给客户端
4.客户端收到 Token 以后可以把它存储起来，比如放在 Cookie 里或者 Local Storage 里
5.客户端每次向服务端请求资源的时候需要带着服务端签发的 Token
6.服务端收到请求，然后去验证客户端请求里面带着的 Token，如果验证成功，就向客户端返回请求的数据
7.APP登录的时候发送加密的用户名和密码到服务器，服务器验证用户名和密码，如果成功，以某种方式比如随机生成32位的字符串作为token，存储到服务器中，并返回token到APP，以后APP请求时，
8.凡是需要验证的地方都要带上该token，然后服务器端验证token，成功返回所需要的结果，失败返回错误信息，让他重新登录。其中服务器上token设置一个有效期，每次APP请求的时候都验证token和有效期。


参考文献：

理论

1.https://www.jianshu.com/p/24825a2683e6
            
2.https://www.cnblogs.com/xuxinstyle/p/9675541.html

3.https://www.cnblogs.com/lufeiludaima/p/pz20190203.html

代码实现

1.https://www.cnblogs.com/chriskwok/p/12599130.html
