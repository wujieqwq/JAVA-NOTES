---





---

# JAVA梳理6(Collection、泛型）


**Collection**
![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_FjnurKXbjJ.png]]
**常用功能**

* 元素存取有序的集合
* 带有索引的集合
* 集合中可以有重复的元素，可以用equals方法

![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_B7ipgUca6A.png]]
**List接口**

* ArrayList
* LinkedList
	* LinkedList方法

![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_N5YI94Zq4u.png]]

### Set接口

* 元素无序，不重复

		Tips:Set集合取出元素方式：Iterator，增强for
HashSet

* 底层由java.util.HashMap支持
* 根据对象的哈希值来确定在集合中的存储位置，因此具有良好的存取和查找性能。保证元素唯一性的方式依赖于：hashCode与equals方法。

存储数据的结构
![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_yAt88N7Xjx.png]]![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_BI9wnYZ3vC.png]]
LinkedHashSet

* 存入的元素有序

### Iterator迭代器

```
public class IteratorDemo {
    public static void main(String[] args) {
        // 使⽤多态⽅式 创建对象
        Collection<String> coll = new ArrayList<String>();
        // 添加元素到集合
        coll.add("串串星⼈");
        coll.add("吐槽星⼈");
        coll.add("汪星⼈");
        // 遍历
        // 使⽤迭代器 遍历 每个集合对象都有⾃⼰的迭代器
        Iterator<String> it = coll.iterator();
        // 泛型指的是 迭代出 元素的数据类型
        while (it.hasNext()) { // 判断是否有迭代元素
            String s = it.next(); // 获取迭代出的元素
            System.out.println(s);
        }
    }
}
```
**泛型**

* 定义和使用含有泛型的类
* 定义和使用含有泛型的方法

![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_OL81pdRmCs.png]]

![[./_resources/JAVA梳理6(Collection、泛型）.resources/msedge_nh7FWcueqw.png]]

