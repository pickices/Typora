# CAS（乐观锁）

CAS,compare and swap的缩写，中文翻译成比较并交换。

> 在JDK 5之前Java语言是靠synchronized关键字保证同步的，这会导致有锁
>
> 锁机制存在以下问题：
>
> （1）在多线程竞争下，加锁、释放锁会导致比较多的上下文切换和调度延时，引起性能问题。
>
> （2）一个线程持有锁会导致其它所有需要此锁的线程挂起。
>
> （3）如果一个优先级高的线程等待一个优先级低的线程释放锁会导致优先级倒置，引起性能风险。
>
> volatile是不错的机制，但是volatile不能保证原子性。因此对于同步最终还是要回到锁机制上来。



## CAS和Synchronized

- synchronized是悲观锁，这种线程一旦得到锁，其他需要锁的线程就挂起的情况就是悲观锁。
- CAS操作的就是乐观锁，每次不加锁而是假设没有冲突而去完成某项操作，如果因为冲突失败就重试，直到成功为止。



## CAS的原理

CAS 操作包含三个操作数 —— 内存位置（V）、预期原值（A）和新值（B）。 

如果内存位置的值与预期原值相匹配，那么处理器会自动将该位置值更新为新值 ；否则，处理器不做任何操作。

无论哪种情况，它都会在 CAS 指令之前返回该位置的值。（在 CAS 的一些特殊情况下将仅返回 CAS 是否成功，而不提取当前值）

CAS 有效地说明了“我认为位置 V 应该包含值 A；如果包含该值，则将 B 放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可“



## CAS例子

1. 内存地址V当中，存储着值为10的变量。

   ![image-20210621220946371](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621220946.png)

2. 此时线程1想要把变量的值增加1。对线程1来说，旧的预期值A=10，要修改的新值B=11。

   ![image-20210621221044669](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221044.png)

3. 在线程1要提交更新之前，另一个线程2抢先一步，把内存地址V中的变量值率先更新成了11。

   ![image-20210621221128081](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221128.png)

4. 线程1开始提交更新，首先进行A和地址V的实际值比较（Compare)，发现A不等于V的实际值，提交失败。

![image-20210621221146269](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221146.png)

5. 线程1重新获取内存地址V的当前值，并重新计算想要修改的新值。此时对线程1来说，A=11，B=12。这个重新尝试的过程被称为自旋。

   ![image-20210621221323779](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221323.png)

6. 这一次比较幸运，没有其他线程改变地址V的值。线程1进行Compare，发现A和地址V的实际值是相等的。

   ![](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221347.png)

7. 线程1进行SWAP，把地址V的值替换为B，也就是12。

   ![image-20210621221421605](https://raw.githubusercontent.com/pickices/Typora/master/image/20210621221421.png)





## CAS的问题

CAS虽然很高效的解决原子操作，但是CAS仍然存在三大问题。ABA问题，循环时间长开销大和只能保证一个共享变量的原子操作

1.  **ABA问题**。因为CAS需要在操作值的时候检查下值有没有发生变化，如果没有发生变化则更新，但是如果一个值原来是A，变成了B，又变成了A，那么使用CAS进行检查时会发现它的值没有发生变化，但是实际上却变化了。ABA问题的解决思路就是使用版本号。在变量前面追加上版本号，每次变量更新的时候把版本号加一，那么A－B－A 就会变成1A - 2B－3A。
2. **循环时间长开销大**。自旋CAS如果长时间不成功，会给CPU带来非常大的执行开销。
3. **只能保证一个共享变量的原子操作**。当对一个共享变量执行操作时，我们可以使用循环CAS的方式来保证原子操作，但是对多个共享变量操作时，循环CAS就无法保证操作的原子性，这个时候就可以用锁。或者有一个取巧的办法，就是把多个共享变量合并成一个共享变量来操作。从Java1.5开始JDK提供了**AtomicReference类来保证引用对象之间的原子性，你可以把多个变量放在一个对象里来进行CAS操作。**

   
