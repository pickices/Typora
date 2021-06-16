#  Callable

>Callabe接口类似于 Runnable。然而，Runnable不返回结果，Callable能抛岀被检查的异常
>
>小结：
>
>1. 可以有返回值
>2. 可以抛出异常
>3. 方法为：call（）

```java
class MyThread implements Callable<Sting> {
    
    @Override
    public String call(){
        //业务代码
        return "";
    }
}

//使用Thread启动Callable
public static void main(String args[]){
    //原理
    new Thread (new Runnable()).start;
    new Thread (new FutureTask<V>()).start();
    new Thread (new FutureTask<V>(Callable)).start();

    //具体使用
    Mythread thread = new Mythread();
    FutureTask futureTask = new FutureTask(thread);  //适配类
    new Thread(futureTask).start();// 
    String str = (String)futureTask.get(); //获取Callable的返回结果,可能会产生阻塞！把他放在最后，或者使用异步通信
}
```







