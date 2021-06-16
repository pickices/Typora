# Lock



## ReentrantLock

使用ReentrantLock锁，JVM将花费较少的时间来调度线程,性能更好。并且具有更好的扩展性（提供更多的子类）

### ReentrantLock与synchronized的区别

- ReentrantLock是一个类，synchronized是JDK内置的关键字
- ReentrantLock可以判断是否拿到了锁，synchronized无法获取锁的状态
- ReentrantLock是显式锁（手动开启和关闭锁，别忘记关闭锁），synchronized是隐式锁，出了作用域自动释放
- ReentrantLock只有代码块锁，synchronized有代码块锁和方法锁
- ReentrantLock可以通过构造函数实现公平锁，synchronized不可以
  
  什么叫公平锁呢？
  也就是在锁上等待时间最长的线程将获得锁的使用权，通俗的理解就是谁排队时间最长谁先执行获取锁。

- ReentrantLock可以让等待锁的线程响应中断，而synchronized不会，线程会一直等待下去（也就是会占用CPU时间片）
- ReentrantLock适合资源竞争激烈的情况使用，synchronized适合竞争不激烈的情况下使用

```java
private final ReentrantLock lock = new ReentrantLock();

lock.lock();

try{
  //业务代码
}catch(Exception e){
  e.printStackTrace();
}finally{
  lock.unlock();
}

```

**优先使用顺序：ReentrantLock>同步代码块（已经进入了方法体，分配了相应资源）>同步方法（在方法体之外）**



## ReentrantReadWriteLock

> 独占锁（排它锁）：写锁，一次只能被一个线程占有
>
> 共享锁：读锁，多个线程可以同时占有

Readwritelock维护一对关联的lock，一个用于只读操作，一个用于写入。readlock可以由多个线程同时使用，writelock只能由一个线程使用

```java
ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

//写锁
readWriteLock.writeLock().lock();
try{
    //业务代码
} catch(Exception e){
    e.printStackTrace();
} finally{
    readWriteLock.writeLock().unlock();
}

readWriteLock.readLock().lock();
try{
    //业务代码
} catch(Exception e){
    e.printStackTrace();
} finally{
    readWriteLock.readLock().unlock();
}
```

### 线程进入读锁的前提条件：

- 没有其他线程的写锁

- 没有写请求或者**有写请求，但调用线程和持有锁的线程是同一个。**

### 线程进入写锁的前提条件：

- 没有其他线程的读锁

- 没有其他线程的写锁
