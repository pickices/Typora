# Session和Cookie

> Session和Cookie的区别

- Cookie：把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）
- Session：把用户的数据写到用户独占的Session中，服务器端保存，且可以保存对象（保存重要的信息，减少服务器资源的浪费）



常用代码：

```java
HttpSession session = req.getSession();
session.setAttribute("kuangshao",new Person("狂少",25));
Person kuangshao = (Person) session.getAttribute("kuangshao");
```