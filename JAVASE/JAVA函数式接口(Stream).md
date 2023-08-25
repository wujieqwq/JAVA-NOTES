---





---

# JAVA函数式接口(Stream)


@FunctionalInterface
  已知: Comparator  Runnable  FileFilter

  Supplier: 生产者
        T get(); // 提供一个T对象

  Consumer: 消费者
        void accept(T t); // 消费 T 对象
        andThen

  Predicate: 用来判断
        boolean test(T t); // 判断 t 对象的逻辑
        and  or  negate

  Function<T, R>: 功能性函数
        R apply(T t); // 将t类型的对象, 转换成R类型
        compose andThen

Stream流: 集合的操作, 里面的方法 自带循环
    延迟方法: 返回值是Stream, 用完一个方法, 可以继续用其他方法
        filter  map  skip  limit  concat  sort
    终结方法: 用完以后流结束了
        foreach  count

1.获取流
Collection集合都可以通过stream()默认方法获取流
Stream接口的静态方法of()获取数组对应的流

Collection获取流
```
import java.util.*;
import java.util.stream.Stream;
public class Demo04GetStream {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        // ...
        Stream<String> stream1 = list.stream();
        Set<String> set = new HashSet<>();
        // ...
        Stream<String> stream2 = set.stream();
        Vector<String> vector = new Vector<>();
        // ...
        Stream<String> stream3 = vector.stream();
    }
}
```
Map获取流
```
import java.util.HashMap;
import java.util.Map;
import java.util.stream.Stream;
public class Demo05GetStream {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        // ...
        Stream<String> keyStream = map.keySet().stream();
        Stream<String> valueStream = map.values().stream();
        Stream<Map.Entry<String, String>> entryStream = map.entrySet().stream();
    }
}
```
数组获取流
```
import java.util.stream.Stream;
public class Demo06GetStream {
    public static void main(String[] args) {
        String[] array = { "张⽆忌", "张翠⼭", "张三丰", "张⼀元" };
        Stream<String> stream = Stream.of(array);
    }
}
//of()方法的参数为可变数组，所以支持数组
```

2.常用方法
过滤filter
```
Stream<String> original = Stream.of("张⽆忌", "张三丰", "周芷若");
Stream<String> result = original.filter(s ‐> s.startsWith("张"));
```
映射map 
```
//转换类型
Stream<String> original = Stream.of("10", "12", "18");
Stream<Integer> result = original.map(str‐>Integer.parseInt(str));
```
跳过前几个skip 
取前几个limit 
```
Stream<String> original = Stream.of("张⽆忌", "张三丰", "周芷若");
Stream<String> result = original.limit(2);
System.out.println(result.count()); // 2
```
组合流concat 
```
Stream<String> streamA = Stream.of("张⽆忌");
Stream<String> streamB = Stream.of("张翠⼭");
Stream<String> result = Stream.concat(streamA, streamB);
```
排序sort
```
//sorted 方法用于对流进行排序。以下代码片段使用 sorted 方法对输出的 10 个随机数进行排序
Random random = new Random();
random.ints().limit(10).sorted().forEach(System.out::println);
```
逐一处理foreach
```
Stream<String> stream = Stream.of("张⽆忌", "张三丰", "周芷若");
stream.forEach(name‐> System.out.println(name));
```
统计个数count
```
Stream<String> original = Stream.of("张⽆忌", "张三丰", "周芷若");
Stream<String> result = original.filter(s ‐> s.startsWith("张"));
System.out.println(result.count()); // 2
```

