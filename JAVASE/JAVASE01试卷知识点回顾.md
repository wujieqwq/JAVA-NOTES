---





---

# JAVASE01试卷知识点回顾


1.Object中重写equals方法
		1.==
		2.类型 instanceof   getClass()
		3.强制类型转换->比较内容
    Object中默认toString()
```
getClass().getName() + '@' + Integer.toHexString(hashCode())
名字全称带包名
```
		HashCode默认方法
				对象的空间地址
3.String
		String trim()：去掉前后空白字符串
		int length()：字符串长度
		char charAt(int index)：获得index位置上的字符
		String substring(int start)：从start开始截取到end
		String substring(int start,int end)：从start开始截取到end

6.正则表达式
```
  1. \d  digit匹配所有的数字，相当于[0-9]
      \D  表示非数字，即\d的反面，相当于[^0-9]
  2. \w word 匹配所有的字母、数字和下划线等[0-9a-zA-Z_]
      \W  取反，表示非字母、数字、下划线[^0-9a-zA-Z_]
  3. \s  space，表示空格
      \S  表示非空格
      替换字符串空格
  4. .  表示匹配任意字符，慎用
      如果要匹配.本身，如何做：需要添加\.表示不转义
```

![[./_resources/JAVASE01试卷知识点回顾.resources/chrome_NyD6fUf2Oc.png]]![[./_resources/JAVASE01试卷知识点回顾.resources/chrome_Su7LeVbK7h.png]]![[./_resources/JAVASE01试卷知识点回顾.resources/chrome_9uiQIg2cba.png]]![[./_resources/JAVASE01试卷知识点回顾.resources/chrome_AfD5A6wBQ8.png]]
10.线程安全的类
		StringBuffer
		HashTable
		Vector
		

13.List遍历
		迭代器 Iterator hasNext() next() remove()
		for循环 for(int i=0;i<list.size();i++) list.get(i)
		foreach for(int i:list)
14.List常用api
		E get(int index)：获得index位置上的内容
		E set(int index,E e)：e替换index上的元素，返回被替换的元素
		void removeAll(Collection col)
		

15.依次删除List中的元素(存在判断，不是删除所有，可以用for)
       依次删除所有，不能用for
16.迭代器中用List的删除方法：
		ConcurrentModificationException：提醒有安全隐患
		删除不成功
19.时间格式化
		SimpleDateFormat extends DateFormat(抽象类)
				yyyy-MM-dd hh:mm:ss
				Date parse(String str):解析
				String format(Date date)：格式化
23.包装类 (常量池问题[稀土掘金](https://juejin.cn/post/6854573216824819719))
		Integer i = new Integer(25);  new对象不用常量池
		Integer i2 = i.intValue();
				i.intValue() -> int 25
				Integer i2 = 25 自动装箱在常量池中
								  = Integer.valueOf(25)
		i和i2地址不同
26.数据结构
		LinkedList:线性链表，从头访问，顺序添加
		ArrayList:数组，自带下标，快速定位
		线性数据结构：数组，链表，队列，双端队列，栈
		

27.数组和List之间转换
		list->array:list.toArray()
		array->list:arrays.asList(array\[\])
		

31.泛型
		Double d = 3.14;
		int a = (int) d; ❌
		泛型只在当前代码块约束
		

35.常用方法
		List subList(int start,int end)
		Queue:
				offer()
				poll()
				peek()
		Deque <https://www.jianshu.com/p/d78a7c982edb>
![[./_resources/JAVASE01试卷知识点回顾.resources/chrome_acLQdgIbN0.png]]
39.
		Comparable:xxx比较xxx
				compareTo(E e)
				当前对象与后一个对象进行比较，如果比较结果为1进行交换，其他不进行交换
		Comparator
				compare(E e1,E e2)
				如果要按照对象的某一个属性进行**升序排序**，那么直接返回o1.属性值-o2.属性值（因为如果第一个数比第二个数大，会返回正值，两个对象要进行交换）
				

44.-
		TreeSet重复判断用Comparator或对象实现Comparable
		HashSet重复判断用equals hashCode
		

		HashSet：
				添加：1.通过hashCode计算位置
						 2.通过equals比较内容
						 3.不相等，添加
				删除：1.通过hashCode计算位置
						 2.通过equals比较内容
						 3.相等，删除
		

45.排序
		数组：Arrays.sort()
		List：Collections.sort() list.sort()
		Set：TreeSet
		Map：TreeMap
		

49.Map常用方法
		put(key,value)
		value    get(key)
		value     remove(key)返回删除的value值
		遍历
		keySet:迭代key
		entrySet:键值对
		values:迭代value

