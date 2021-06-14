# Lamda表达式

Lamda表达式是在JDK8中新加入的特性

## 函数式接口

- 任何**接口**，如果只包含**—个抽象方法**，那么它就是一个函数式接口
- 对于函数式接口，我们可以通过Lambda表达式来创建该接口的对象。



## Lamda

```java
interface ILove(){
  void love(int a);
}

//原始Lamda表达式
ILove love = (int a)->{
  System.out.println("i love you"+a);
}

//简化参数类型
love = (a)->{
  System.out.println("i love you"+a);
}

//简化小括号
love = a->{
  System.out.println("i love you"+a);
}

//简化花括号
ILove love = a->System.out.println("i love you"+a);
```

**注意：**

1. Lambda表达式只能有一行代码的情况下才能筒化成为一行。如果有多行,那么就用代码块包裹
2. 必须是接口为函数式接口
3. 多个参数也可以去掉参数类型，要去掉就都去掉,必领加上括号
