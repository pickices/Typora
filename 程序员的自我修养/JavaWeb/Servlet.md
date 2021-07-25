# Servlet

## 简介

Servlet是sun公司开发动态web的一门技术
Sun在这些AP中提供一个接口叫做：Servlet。如果开发一个 Servlet程序，只需要完成两个小步骤：

- 编写一个类,实现Servlet接口
- 把开发好的Java类部署到web服务器中

**把实现了Servlet接口的Java程序叫做Servlet**



## 生命周期

Servlet的生命周期分为5个阶段：加载、创建、初始化、处理客户请求、卸载。

1. 加载：容器通过类加载器使用servlet类对应的文件加载servlet

2. 创建：通过调用servlet构造函数创建一个servlet对象

3. 初始化：调用init方法初始化

4. 处理客户请求：每当有一个客户请求，容器会创建一个线程来处理客户请求
5. 卸载：调用destroy方法让servlet自己释放其占用的资源