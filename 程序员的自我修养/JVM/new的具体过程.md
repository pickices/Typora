# new的具体过程



1. 首先到常量池中找类的带路径全名，然后检查对应的字节码是否已被加载，解析，验证，初始化，如果没有先执行类加载过程(class.forname())。
2. 类加载过程完成后，虚拟机会为对象分配内存。分配内存有两种方式，根据使用的垃圾收集器的不同使用不同的分配机制。
   - 指针碰撞，当虚拟机使用复制算法或标记整理算法实现的垃圾收集器时，内存区域都是规整的，这时候使用指针碰撞分配内存，用过的内存放在一边，空闲的内存在另一边，中间用一个指针作为分界点，当需要为新对象分配内存时只需把指针向空闲的一边移动一段与对象大小相等的距离。
   - 空闲列表，当虚拟机使用标记清除算法实现的垃圾收集器时，内存都是碎片化的，那虚拟机就要记录哪块内存是可用的，当需要分配内存时，找一块足够大的内存空间给对象实例，并更新记录。

3. 设置对象头信息，如所属类，元数据信息，哈希码，gc分代年龄，等等。
4. 调用对象的init()方法,根据传入的属性值给对象属性赋值。
5. 在线程栈中新建对象引用，并指向堆中刚刚新建的对象实例。

![截图](C:\Users\拾荒老冰棍\Desktop\GC回收算法\aeae1cf809e23b63d7511a7bdfd21f0f.png?lastModify=1623664080)

![](https://raw.githubusercontent.com/pickices/Typora_Image/master/picgo/20210614175019.png)

![image-20210614175138553](https://raw.githubusercontent.com/pickices/Typora_Image/master/picgo/20210614175138.png)

![截图](C:\Users\拾荒老冰棍\Desktop\GC回收算法\aeae1cf809e23b63d7511a7bdfd21f0f.png?lastModify=1623664080?lastModify=1623664296)

![截图](C:\Users\拾荒老冰棍\Desktop\GC回收算法\aeae1cf809e23b63d7511a7bdfd21f0f.png?lastModify=1623664080?lastModify=1623664296)