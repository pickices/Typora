# GC回收算法

## 年轻代和老年代的GC

### MinorGC

从年轻代空间（包括 Eden 和 Survivor 区域）回收内存被称为 Minor GC，也叫Young GC。因为Java对象大多具备朝生夕死的特征，所以MinorGC非常频繁，一般回收速度也比较快。一般采用复制算法。
Minor GC触发条件
Eden区域满了，新生对象需要分配到新生代的Eden，当Eden区的内存不够时需要进行MinorGC

### Major GC/Full GC

MajorGC：清理老年代
FullGC：Full GC可以看做是Major GC+Minor GC共同进行的一整个过程，是清理整个堆空间。Full GC的速度一般会比 Minor GC慢10倍以上。一般用的是标记整理和标记清除算法



## 复制算法

1. 初始阶段，对象分配在Eden区（大对象直接进入老年代，通过-XX:PretenureSizeThreshold配置），此时S0和S1是空的（圆圈中的数字代表对象的年龄）
   ![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200608.png)
   
2. 当Eden区满了之后，进行MinorGC，经过扫描与标记，不再存活的对象被清除，存活的对象进入Survivor中的S0并且对象年龄+1，此时Eden被清空，S1是空的
   ![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200624.png)
   
3. 然后随着对象增多又一次MinorGC后，Eden区和S0区存活的对象进入S1区并且对象年龄+1，Eden和S0区被清空
   ![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200626.png)
   
4. 又一次MinorGC后，和上面步骤类似，Eden区和S1区存活的对象进入S0区并且对象年龄+1，Eden和S1区被清空
   ![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200638.png)
   
5. 对象每熬过一次MinorGC其年龄就会加1，达到年龄阈值（可通过参数-XX:MaxTenuringThreshold配置，默认为15）的年轻代对象会晋升到老年代，随着进入老年代的对象越来越多，当老年代内存不够用时会触发MajorGC

   ![5e67c64bf0998cd53b483778a60af7fe](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614201353.png)



## 标记清除算法

标记清除算法的执行过程分为两个阶段：标记阶段、清除阶段。

- 标记阶段会通过可达性分析将不可达的对象标记出来。

![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200645.png)

- 清除阶段会将标记阶段标记的垃圾对象清除。

![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200650.png)

#### 缺点：

- 执行效率不高，需要进行两次遍历
- 这种方式清理出来的空闲内存是不连续的，产生内存碎片，需要维护一个空闲列表



## 标记压缩算法

标记压缩算法是目的在于优化标记清除算法，可以解决标记清除算法的内存碎片问题。其算法可以看作三步：

- 标记垃圾对象

![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200656.png)

- 清除垃圾对象

![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200720.png)

- 内存碎片整理（可以在多次标记清除后再进行整理）

![截图](https://raw.githubusercontent.com/pickices/Typora/master/image/20210614200725.png)



## 总结

内存效率：复制算法 > 标记清除算法 > 标记压缩算法（时间复杂度）
内存整齐度：复制算法 = 标记压缩算法 > 标记清除算法
内存利用率：标记压缩算法 = 标记清除算法 > 复制算法

> 没有最好的算法，只有最合适的算法---->分代收集算法

### 分代收集算法

**年轻代：**

- 存活率低
- 大多使用复制算法

**老年代：**

- 空间大，存活率高
- 使用标记清除+标记压缩混合算法