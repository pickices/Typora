## Volatile

Volatile是Java虚拟机提供的轻量级同步机制

1. 保证可见性（线程工作区内存的变量可以感知到外部内存的变量的修改）
2. **不保证原子性**

原子性：不可分割
线程在执行任务的时候，不能被打扰，也不能被分割。要么同时成功，要么同时失败

> **如果不使用synchronized和lock，怎么保证原子性**
>
> - 不使用非原子性的操作，比如num++,num--
>
> - 使用原子类（AtomicInteger,AtomicLong...）
>
>   ```java
>   private volatile static AtomicInteger num = new AtomicInteger();
>   num.getAndIncrement(); //取代num++
>   ```
>
>   

3. 禁止指令重排

指令重排：计算机并不是按照我们写的程序的顺序执行的，顺序可能被重新排列

**处理器在进行指令重排的时候，会考虑数据之间的依赖性**