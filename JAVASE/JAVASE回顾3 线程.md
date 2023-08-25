---





---

# JAVASE回顾3 线程


1.线程创建方式
		1.创建线程类

* 定义Thread类的子类，重写run()方法，run()的方法体代表该线程需要完成的任务
* 创建Thread子类的实例，即线程对象
* 调用线程对象的start()方法启动该线程

```
线程类
public class MyThread extends Thread {
    // 定义指定线程名称的构造⽅法
    public MyThread(String name) {
        // 调⽤⽗类的String参数的构造⽅法，指定线程的名称
        super(name);
    }
    /**
    * 重写run⽅法，完成该线程执⾏的逻辑
    */
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
        System.out.println(getName() + "：正在执⾏！" + i);
        }   
    }
}
------------------------------------------------
测试类
public class Demo01 {
    public static void main(String[] args) {
        // 创建⾃定义线程对象
        MyThread mt = new MyThread("新的线程！");
        // 开启新线程
        mt.start();
        // 在主⽅法中执⾏for循环
        for (int i = 0; i < 10; i++) {
            System.out.println("main线程！" + i);
        }
    }
}
```
		2.java.lang.Runnable 重写run方法

* 1.实现Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程知兴体
* 2.创建Runnable实现类的实例，并以此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象
* 3.调用线程对象的start()方法来启动线程

```
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
        System.out.println(Thread.currentThread().getName() + " " + i);
        }
    }
}
----------------------------------------------------
public class Demo {
    public static void main(String[] args) {
        // 创建⾃定义类对象 线程任务对象
        MyRunnable mr = new MyRunnable();
        // 创建线程对象
        Thread t = new Thread(mr, "⼩强");
        t.start();
        for (int i = 0; i < 20; i++) {
          System.out.println("旺财 " + i);
        }
    }
}
```
		3.匿名内部类
```
public class NoNameInnerClassThread {
    public static void main(String[] args) {
        // new Runnable() {
        //    public void run() {
        //        for (int i = 0; i < 20; i++) {
        //            System.out.println("张宇:" + i);
        //        }
        //    }
        // }; //‐‐‐这个整体 相当于new MyRunnable()
        Runnable r = new Runnable() {
            public void run() {
                for (int i = 0; i < 20; i++) {
                    System.out.println("张宇:" + i);
                }
            }
        };
        new Thread(r).start();
        for (int i = 0; i < 20; i++) {
            System.out.println("费⽟清:" + i);
        }
    }
}
```
		4.实现Callable接口

* call()可以有返回值的
* call()可以抛出异常，被外面的操作捕获，获取异常的信息
* Callable是支持泛型的

		5.线程连接池

### Thread和Runnable的区别

		如果一个类继承Thread，则不适合资源共享。但是如果实现了Runnable接口的话，则容易实现资源共享。
		Runnable接口的优势
		1.适合多个相同的程序代码的线程去共享同一个资源
		2.可以避免java中的单继承局限性
		3.增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立
		4.线程池只能放入实现Runnable或Callable类线程，不能直接放入继承Thread的类
		Tips：java中，每次程序运行至少启动2个线程。一个main，一个垃圾收集线程。每当java命令执行一个类的时候，实际上都会启动一个JVM,每个JVM在操作系统中启动了一个进程。
		

		

2.线程同步
		1.synchronized关键字

* 同步方法

```
synchronized(同步锁) {
    需要同步操作的代码
}
```

* 同步代码块

```
public synchronized void method() {
    可能会产⽣线程安全问题的代码
}
```
		2.lock接口

* lock()加同步锁
* unlock()释放同步锁
* 实现类是ReentrantLock（可重入锁）
* 一般来说，使用Lock必须在try{}catch{}块中进行，并且将释放锁的操作放在finally块中进行

```
private static Lock lock = new ReentrantLock();

    public static void main(String[] args) {
        lock.lock();
        try{
            System.out.println("获取锁成功！！");
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            System.out.println("释放锁成功");
            lock.unlock();
        }
    }


```
3.线程状态
![[./_resources/JAVASE回顾3_线程.resources/msedge_7Eb9FrF8ME.png]]![[./_resources/JAVASE回顾3_线程.resources/线程状态.png]]
		1.sleep() 计时等待

* 让其他线程有机会执行，可以将Thread.sleep()的调用放线程run()之内，保证该线程运行过程中会睡眠
* sleep与锁无关，线程睡眠到苏醒，进入Runnable(可运行)状态
* 不能保证线程睡眠到期后立即执行

		

		2.wait(long) 计时等待
		3.join(long) 计时等待
		4.wait()无限等待

* 只有已经获取锁的线程，才可以调用锁的wait()、notify()方法，否则会抛出异常IllegalMonitorStateException
* wait()与notfiy()方法必须要由同一个锁对象调用
* wait()与notfiy()方法属于Object类方法，锁对象可以是任意对象

		5.notfiy() notifyAll() 唤醒

* 唤醒后变为blocked状态，需要获得锁之后进入Runnable

		6.join()无限等待

* 使主线程(或者说调用t.join()的线程)进入等待池并等待t线程执行完毕后才会被唤醒

		7.守护线程

* 守护线程不能持有任何需要关闭的资源，例如打开文件等，因为虚拟机退出时，守护线程没有任何机会来关闭文件，这会导致数据丢失
* 处理无线循环的线程，设置为守护线程后，所有非守护线程执行完毕，虚拟机退出

```
Thread t = new MyThread();
t.setDaemon(true);
t.start();
```
4.线程池
```
┌─────┐ execute  ┌──────────────────┐
│Task1│─────────>│ThreadPool        │
├─────┤          │┌───────┐┌───────┐│
│Task2│          ││Thread1││Thread2││
├─────┤          │└───────┘└───────┘│
│Task3│          │┌───────┐┌───────┐│
├─────┤          ││Thread3││Thread4││
│Task4│          │└───────┘└───────┘│
├─────┤          └──────────────────┘
│Task5│
├─────┤
│Task6│
└─────┘
  ...
```
		Java标准库提供了`ExecutorService`接口表示线程池，它的典型用法如下：
```
// 创建固定大小的线程池:
ExecutorService executor = Executors.newFixedThreadPool(3);
// 提交任务:
executor.submit(task1);
executor.submit(task2);
executor.submit(task3);
executor.submit(task4);
executor.submit(task5);
```

