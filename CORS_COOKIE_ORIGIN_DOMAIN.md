# cors_cookie

一些关于CORS， Cookie，Domain，Origin 以及第三方Cookie
---
关于Cookie，
平时使用Cookie其实比较少， 由于最近几年都是新项目， 没有历史包袱，所以均为无状态+JWTToken的模式



## Origin Domain SameSite
### Origin
[Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin): <scheme> "://" <hostname> [ ":" <port> ]

[hostname](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin)
The domain name of the server (for virtual hosting) or the IP.
  
### domain
[域名基础知识](https://support.google.com/a/answer/2573637?hl=zh-Hans#B)
[Domain name basics](https://support.google.com/a/answer/2573637?hl=en)


related: [DNS(The Domain Name System)](https://en.wikipedia.org/wiki/Domain_Name_System)
related: [Browsers limit the number of HTTP connections with the same domain name](https://docs.pushtechnology.com/cloud/latest/manual/html/designguide/solution/support/connection_limitations.html#:~:text=Browsers%20limit%20the%20number%20of,allow%20six%20connections%20per%20domain.)

### subdomain
域名： google.com
子域名： support.google.com


## CORS
Cross-**Origin** Resource Sharing
[link](https://developer.mozilla.org/zh-CN/docs/Glossary/CORS)
CORS针对的是Origin，而不是domain


## Cookie
Server的response header 里面有
```Set-Cookie: name=value; domain=mydomain.com```
or
```Set-Cookie: name=value```
这样下次client再去向server发http的时候就会带上cookie。
subdomain 会带上 他自己 和 domain的 cookie

In RFC 2109, a domain without a leading dot meant that it could not be used on subdomains, and only a leading dot (.mydomain.com) would allow it to be used across multiple subdomains(but not the top-level domain).

However, all modern browsers respect the newer specification RFC 6265, 
and will ignore any leading dot, meaning you can use the cookie on subdomains as well as the top-level domain.

subsubdomain会带上 他自己 和 subdomain的 和 domain的cookie

而domain不会带subdomain已经subsubdomain的cookie

### 第三方Cookie

是否允许第三方去写cookie，并在下次请求第三方时带上其cookie
Safari默认禁止， chrome也将于几年后禁止
何为第三方？
What's the third-party cookie?
非当前domain的即为第三方cookie
abc.com, a.abc.com, b.abc.com aa.a.abc.com 这些都属于第一方cookie
bcd.com是属于第三方cookie

### 谁可以访问cookie
浏览器请求 和 JavaScript
HttpOnly指示cookie将不能通过JavaScript的document.cookie编程接口访问，这样可以缓解对跨站点脚本（XSS）的攻击。


## 跨域Cookie Cross-Origin Cookie
带上自己的Cookie去送往其他的server是不安全的。


跨域默认情况下，浏览器是不应该带上cookie的
但是由于资源和api的分离，API的请求很可能和静态资源造成了Cross-Origin
这时候需要 client端和server端都做一些事情
Client端需要带上 WithCreditial
Server端需要设置这个header  Access-Control-Allow-Credentials: true
并且设置 Access-Control-Allow-Origin: <client的origin>

----
to be continue
