---





---

# JAVASE02试卷知识点回顾


1.
  FileOutputStream(文件路径): 如果文件不存在, 创建新文件; 文件存在, 清空内容写入
  FileOutputStream(文件路径, true): 文件存在, 在末尾追加内容

  BufferedOutputStream(OutputStream)
        带缓冲区的输出流, 必须刷新缓冲区才能真正写出 flush()
  write(int)  write(byte\[\])

   PrintWriter(xxx,true) 构造器设置自动刷新缓冲区

2.序列化接口 Serializable
  没有方法, 没有字段(静态常量); 就是为了标识可以序列化
  transient: 忽略属性的值

3.try ... catch ... finally
  catch 可以有多个, 如果多个异常有父子关系的, 子类异常必须在前面捕获
                  如果多个异常没有关系, 顺序无所谓了
  finally 不论有没有异常, 都会执行
  已检查异常, 运行时异常
  必须处理已检查异常

  基类为 Throwable，Error 和 Exception 继承 Throwable，
  RuntimeException 和 IOException 等继承 Exception

6.File类: 表示文件或者目录
  isFile() isDirectory() isExists() mkdir() mkdirs()
  listFiles() createNewFile() delete()
  listFiles(FileFilter)

7.方法重写:
  父类A: protected Number method1(int a) throws IOException {}
  子类B: protected/public -> 访问修饰符必须更开放
        返回值: Number/Integer/Double        如果是基本数据类型则必须一样
        方法名, 参数: 必须一样
        throws IOException/FileNotFoundException 不能多于父类的异常

  private default protected public

  补: Number 是 Integer/Double/Short...数字类的包装类型的父类

补充：
重写规则

* 参数列表必须完全与被重写方法的相同；
* 返回类型必须完全与被重写方法的返回类型相同；
* 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为public，那么在子类中重写该方法就不能声明为protected。
* 父类的成员方法只能被它的子类重写。
* 声明为final的方法不能被重写。
* 声明为static的方法不能被重写，但是能够被再次声明。
* 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为private和final的方法。
* 子类和父类不在同一个包中，那么子类只能够重写父类的声明为public和protected的非final方法。
* 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。
* 构造方法不能被重写。
* 如果不能继承一个方法，则不能重写这个方法。

重载规则：

	被重载的方法必须改变参数列表(参数个数或类型或顺序不一样)。
	
	被重载的方法可以改变返回类型。
	
	被重载的方法可以改变访问修饰符。
	
	被重载的方法可以声明新的或更广的检查异常。
	
	方法能够在同一个类中或者在一个子类中被重载。
	
	无法以返回值类型作为重载函数的区分标准。
	

![[./_resources/JAVASE02试卷知识点回顾.resources/chrome_4mTaeYNhJO.png]]
15.
   Thread中默认的run方法实现:
   public void run() {
        if (target != null) {
            target.run();
        }
   }

16.线程进入阻塞状态
    join()
    sleep()
    wait()
    锁
    IO阻塞

24.
   Collections.sort(list, Comparator)
   Arrays.sort(array): 数组里的元素类型必须是可比较的 Comparable
   Arrays.sort(array, comparator)
    Comparator: compare(o1, o2)

26.
		成员变量有初始值    可能只出现空指针
		局部变量无初始值    可能出现编译失败

25.RandomAccessFile
      FileInputStream FileOutputStream ObjectInputStream ObjectOutputStream

32.守护线程 Daemon
   前置线程结束后, 守护线程自动结束

33.线程的生命周期
   new -> start

36.IO的创建时, 通常会有FileNotFoundException
   IO在读写时, 通常会有IOException

46.BufferedReader  PrintWriter
    a: readLine() 一行就是一个单词 -> ArrayList
    b: readLine() 读完一行 split("\\\\s+") -> ArrayList

    for(int i = 0; i < 最小长度)
        a.get(i) b.get(i)  print
    将剩余的部分一次性写入

