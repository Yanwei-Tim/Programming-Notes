# HTTP-范围请求

在 HTTP/1.1（RFC2616） 之上，支持了范围请求。范围请求允许服务器只发送 HTTP 消息的一部分到客户端。范围请求在传送大的媒体文件，或者与文件下载的断点续传功能搭配使用时非常有用。

范围请求的具体应用场景

- 多线程下载：对单个资源，开启多个线程进行下载，每个线程只下载整个资源的一部分，这样就要求服务器支持范围请求。
- 断点续传：如果一个资源已经下载了 90%，但由于一些原因下载被中断了，如果服务器不支持范围请求，客户端就必须重新下载这个资源。

HTTP范围请求设计以下几个知识点：

- 判断服务器是否支持范围请求：如果服务器响应中含有 `Accept-Ranges: bytes` 首部，那么说明其自持范围请求。
- 客户端如何使用范围请求：客户端使用 `Ranges` 并且处理 `206` 响应码。
- 范围请求与文档过期处理：是使用 E-Tag 或 Last-Modified 首部来确定已经下载的部分是否过期。


关于HTTP范围请求下面连接已经总结得非常全面，具体可以参考下面连接，也可以试着编写一个多线程端点续传程序来加深对HTTP范围范围请求的理解。

## 引用

- [图解：HTTP 范围请求，助力断点续传、多线程下载的核心原理](https://www.cnblogs.com/plokmju/p/http_range.html)
- [HTTP请求范围](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Range_requests#%E6%A3%80%E6%B5%8B%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E6%98%AF%E5%90%A6%E6%94%AF%E6%8C%81%E8%8C%83%E5%9B%B4%E8%AF%B7%E6%B1%82)