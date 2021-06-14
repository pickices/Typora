# Request和Response

web服务器接收到客户端的http请求后，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，和代表响应的一个HttpServletResponse对象

- 如果要获取客户端请求过来的参数：HttpServletRequest
- 如果要给客户端响应一些信息：HttpServletResponse

## HttpServletResponse

### 常见应用

- 向浏览器输出消息
- 下载文件

1. 获取路径
2. 获取文件名
3. 让浏览器支持下载
4. 获取FileInputStream下载输入流
5. 创建缓冲区
6. 获取ServletOutputStream对象
7. 将ServletOutputStream流写入buffer缓冲区
8. 使用ServletOutputStream将缓冲区中的数据输出到客户端

- 验证码实现
- 重定向

```java
void sendRedirect(String var1) throws IOException;
```

> 重定向和转发的区别？

- 相同点
  - 页面都会实现跳转
- 不同点
  - 请求转发的时候，url不会产生变化
  - 重定向时候,，url会发生变化

## HttpServletRequest

### 常见应用

- 获取客户端传递的参数

```java
req.getparameter(String s)
req.getparameterValues(String s)
```
