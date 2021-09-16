# JVM参数

-Xmx10240m：代表最大堆

-Xms10240m：代表最小堆

-Xmn5120m：代表新生代

-XXSurvivorRatio=3：代表Eden:Survivor = 3 ，根据Generation-Collection算法(目前大部分JVM采用的算法)，一般根据对象的生存周期将堆内存分为若干不同的区域，一般情况将新生代分为Eden ，两块Survivor；计算Survivor大小，Eden:Survivor = 3，总大小为5120，Survivor有两份，即5120/5*2

