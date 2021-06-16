# native关键字

> 凡是带有native关键字的，说明JAVA的作用范围达不到了，回去调用底层C语言的库！
>
> 会进入本地方法栈，调用本地方法接口（JNI）
>
> JNI：
>
> - 扩展JAVA的使用，融合不同的编程语言给JAVA使用。
> - 在内存区域开辟一块标记区域：Native Method Stack，登记native方法
> - 在执行native方法的时候，通过JNI接口加载本地方法库的方法

