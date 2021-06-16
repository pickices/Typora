# JUC的等待唤醒

![image-20210615154017107](https://raw.githubusercontent.com/pickices/Typora/master/image/20210615154947.png)

- `Condition`取代了`Object`的监视器方法（ [`wait`](../../../lang/Object.html#wait()) ， [`notify`](../../../lang/Object.html#notify())和[`notifyAll`](../../../lang/Object.html#notifyAll())  ），通过与Lock的组合实现了`synchronized`与`wait`和`notify`的效果。  如果`Lock`替换了`synchronized`方法和语句的使用，则`Condition`将替换Object监视方法的使用。 
- `Condition`的优势：
  - Condition可以精准地通知和唤醒线程 



```java
Lock lock = new ReentrantLock();
Condition condition = lock.newCondition();
condition.await();
condition.signalAll();
```

