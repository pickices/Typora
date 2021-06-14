# HashMap

<br/>

### 基本常量

- DEFAULT_INITIAL_CAPACITY ：默认的hash表长度，为16
- MAXIMUM_CAPACITY：hash表的最大长度，取值范围为2-2^30
- DEFAULT_LOAD_FACTOR：默认负载因子
- TREEIFY_THRESHOLD：当桶中元素个数超过这个值时，需要使用红黑树节点替换链表节点
- UNTREEIFY_THRESHOLD：当扩容时，桶中元素个数小于这个值，就会把树形的桶元素 还原（切分）为链表结构
- MIN_TREEIFY_CAPACITY：
  - 当哈希表中的容量大于这个值时，表中的桶才能进行树形化
  - 否则桶内元素太多时会扩容，而不是树形化
  - 为了避免进行扩容、树形化选择的冲突，这个值不能小于 4 * TREEIFY_THRESHOLD
