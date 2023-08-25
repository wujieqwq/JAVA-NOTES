---





---

# JAVA梳理8(Map)


与Collection的不同
![[./_resources/JAVA梳理8(Map).resources/msedge_7mLQ96Ydht.png]]
Map结构
![[./_resources/JAVA梳理8(Map).resources/msedge_h4dUcyxV9R.png]]
Map子类

* HashMap:存储数据采用的哈希表结构，元素的存取顺序不能保证一致。由于要保证键的唯一、不重复，需要重写键的hashCode()方法、equals()方法。
* LinkedHashMap:存储结构采用哈希表结构+链表结构。通过链表结构可以保证元素的存取顺序一致；通过哈希表结构保证键的唯一，需重写键的hashCode()方法、equals()方法。

常用方法
![[./_resources/JAVA梳理8(Map).resources/msedge_Xn3b56prfg.png]]
Tips:使用put方法，若指定的键在集合中没有，则没有这个键对应的值，返回null,并把指定的键值添加到集合中。
若指定的键存在，则返回值为集合中键对应的值，并把指定键所对应的值，替换成指定的新值。

Map遍历
1.Map遍历键找值
		1.1获取Map中所有的键 keySet()
		1.2遍历键的Set集合，得到每一个键
		1.3根据键，获取对应值 get(K key)
```
public class MapDemo01 {
    public static void main(String[] args) {
        // 创建Map集合对象
        HashMap<String, String> map = new HashMap<String,String>();
        //添加元素到集合
        map.put("胡歌", "霍建华");
        map.put("郭德纲", "于谦");
        map.put("薛之谦", "⼤张伟");
        // 获取所有的键 获取键集
        Set<String> keys = map.keySet();
        // 遍历键集 得到 每⼀个键
        for (String key : keys) {
            // key 就是键
            // 获取对应值
            String value = map.get(key);
            System.out.println(key + "的CP是:" + value);
        }     
    }
}
```

![[./_resources/JAVA梳理8(Map).resources/msedge_Nah9FpEMQk.png]]
2.Map遍历键值对
		Entry键值对对象
![[./_resources/JAVA梳理8(Map).resources/msedge_y1fg9Gw5jg.png]]
		2.1获取所有键值对对象 entrySet()
		2.2遍历包含键值对对象的Set集合
		2.3通过键值对对象获取Entry对象的键与值 getKey() getValue()
```
public class MapDemo02 {
    public static void main(String[] args) {
        // 创建Map集合对象
        HashMap<String, String> map = new HashMap<String,String>();
        // 添加元素到集合
        map.put("胡歌", "霍建华");
        map.put("郭德纲", "于谦");
        map.put("薛之谦", "⼤张伟");
        // 获取 所有的 entry对象 entrySet
        Set<Entry<String,String>> entrySet = map.entrySet();
        // 遍历得到每⼀个entry对象
        for (Entry<String, String> entry : entrySet) {
            // 解析
            String key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + "的CP是:" + value);
        }
    }
}
```

![[./_resources/JAVA梳理8(Map).resources/msedge_lFtnkOsLfU.png]]

JDK9及之后
of()方法
```
public class HelloJDK9 {
    public static void main(String[] args) {
        Set<String> str1=Set.of("a", "b", "c");
        // str1.add("c"); 这⾥编译的时候不会错，但是执⾏的时候会报错，因为是不可变的集合
        System.out.println(str1);
        Map<String, Integer> str2 = Map.of("a", 1, "b", 2);
        System.out.println(str2);
        List<String> str3 = List.of("a", "b");
        System.out.println(str3);
    } 
}
```
Tips:
1.of()方法只是Map,List,Set这三个接口的静态方法，其父类和子类实现没有这类方法例如HashSet,ArrayList等
2.返回的集合是不可变的

