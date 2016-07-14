title: HTTP状态码
date: 2016-02-09 15:48:36
categories: 归纳整理 #文章文类
tags: [HTTP] #文章标签，多于一项时用这种格式
---
状态码：客户端访问服务器时返回的状态码

格式：状态码通常是由三位数字和原因短语组成，其中第一位数字为响应类别，比如：
200 OK 

响应类别有以下5种：
- 1XX Information（信息类状态码） 接收的请求正在处理
- 2XX Success （成功状态码）请求正常处理完毕
- 3XX Redirection （重定向状态码）需要进行附加操作以完成请求
- 4XX Client Error （客服端错误状态码）服务器无法处理请求
- 5XX Server Error （服务端错误状态码）服务器处理请求出错

常用状态码

1. 2XX 成功 
- 200 OK表示客户端发来的请求在服务器上被正常处理了 
- 204 No Content 服务器接受的请求已经处理成功，但返回的响应报文中不含实体的主体成分 
- 206 Partial Content 客户端进行了范围请求，服务器成功执行了这部分GET请求 

2. 3XX 重定向 
- 301 Moved Permanently 永久性重定向 
- 302 Found 临时性重定向 
- 303 See Other 请求对应的资源存在着另一个URL，应使用GET方法重新获取请求的资源
- 304 Not Modify 客户端发送附加条件的请求时，服务器端允许请求访问资源 
- 307 Temporary Redirect 临时性重定向 

3. 4XX 客户端错误 
- 400 Bad Request 请求报文中存在语法错误 
- 401 Unauthorized 权鉴失败，需要有HTTP认证的认证信息
- 403 Forbidden 请求的资源被服务器拒绝了
- 404 Not Found 服务器无法找到该资源 

4. 5XX 服务器错误
- 500 Internal Server Error 服务器执行请求时发生错误
- 502 Bad Gateway PHP没有认证版本
- 503 Service Unavailable 服务器暂时处于超负载或正在进行停机维护，现在无法处理请求 
