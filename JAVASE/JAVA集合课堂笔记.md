---





---

# JAVA集合课堂笔记


集合架构:
  Collection(I) -> Iterable(I)
    |- List(I): 允许重复, 有序的 add(index, object) get(index) set(index, object) remove(index)
        |- ArrayList: 初始容量10, 扩容机制1.5
        |- LinkedList
        |- Vector: 带 synchronized(锁) 线程安全, 效率低
    |- Set(I): 不允许重复\[Set的底层就是Map\]
        |- HashSet: 无序, 不允许重复\[底层就是HashMap\]
        |- TreeSet: 排序的, 底层是二叉树, 添加时就需要比较 \[TreeMap\]
        |- LinkedHashSet: \[LinkedHashMap\]
    |- Queue(I)
		|-Deque
		      |-LinkedList
		      |-Stack

排序相关:
    Arrays.sort(数组): 自然顺序的升序排序
        1.将数组里的元素先转换成Comparable类型
        2.再通过compareTo方法, 和数组里的另一个元素比较
    Arrays.sort(数组, Comparator 比较器):
        根据比较器的规则来排序
    Collections.sort(List), Collections.sort(list, comparator)
    list.sort(), list.sort(comparator)
支持排序的集合:
    List: Collections.sort    List->sort
    Set: TreeSet
Queue: 队列(先进先出)
    offer poll peek
Deque: 双端队列
    offerFirst/offerLast(offer)
    pollFirst(poll)/pollLast
    栈: push pop

    Comparable: 对象是可比较的
    Comparator: 比较器, 功能是比较两个对象

二叉树:
  本身自带特性: 左 < 中 < 右
  遍历方式: 左  右
    先序遍历: 中  左  右
    中序遍历: 左  中  右 -> 由小到大
    后序遍历: 左  右  中

递归: 另一种循环, 自己调用自己
  1.循环体, 递归的事情, 公式
  2.参数变化规律
  3.结束条件

