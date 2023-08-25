---





---

# JAVA线程2


![[./_resources/JAVA线程2.resources/线程状态.png]]

线程:
    程序: 软件(服务)
    进程: 打开的程序, 消耗内存
    线程: 进程中的任务单位, 一个进程至少会有一个线程
         可以"同时"执行

开启多线程: Thread
    1.继承父类 Thread
    2.实现父接口  Runnable
    3.匿名内部类

多线程的生命周期:
  new: 创建对象
  start: 进入到就绪状态
  从就绪池中随机选择一个线程执行: 进入到运行状态
        cpu给一个线程分配时间片(随机)
        cpu时间片到期时, run方法可能会在任意位置中止, 并且线程回到就绪状态
                       记录当前run方法的执行位置(标记)

常用API:
  1.可以获得当前线程对象 static  currentThread()
  2.获得线程的名字  String getName()
  3.优先级(了解): 1~10从小到大, 默认是5
    setPriority(int )
    作用: 优先级高只是提高了线程被CPU选择的概率
  4.static yield(): 主动归还cpu时间片
  5.static sleep(long time)
  6.void setDaemon(boolean): 设置守护线程(了解)
      守护线程: 前置线程结束后, 守护线程自动结束
      前台线程/前置线程: 所有前置线程都结束, 进程才算结束; 线程默认就是前置线程
      已知守护线程: GC 垃圾回收机制

在线程中调用普通方法, 不会改变线程, 每个线程都会为这个方法在栈中开辟一个独立空间
    每个线程的每个方法, 空间都是独立的, 方法中的临时变量, 都不会有影响
    只有堆中的数据, 有可能被线程共享

线程同步: 多个线程, 共享资源
  案例: 两个线程, 窗口1 和 窗口2, 都是负责卖票的
       票的总数 100, 卖完为止
  问题: 会出现重复票, 或者不存在的票
  原因: 代码在出票过程中, 会随时被打断(中止)
  总结: 线程同步的不安全问题    StringBuilder StringBuffer,  HashMap Hashtable, ArrayList Vector
  解决方法: 添加同步锁 synchronized
       synchronized: 每一个对象上, 都有一把锁; 同一时间只能被一个线程获得(使用), 效率会降低
             原则上, 锁的范围越小越好
             可以锁方法: this对象锁
             锁代码块: 对象通常也是this
       Lock锁

线程的通信:
    join: 单向通信, 线程a 主动等待线程b结束, 线程b 不知道
    wait/notify: Object中的
    生产者 和 消费者

sleep和wait的区别:
  1.所属类的区别
  2.参数的区别
  3.唤醒方式不同
  4.锁的区别: sleep不会释放锁, wait会释放锁

Object:
  toString equals hashCode
  getClass clone finalize
  wait \* 3  notify notifyAll: 在使用时, 必须加锁
  wait: 无限等待, 只能通过notify notifyAll唤醒
        计时等待, 可以时间到了自动醒, 也可以被notify notifyAll唤醒

线程池:
       提前准备了几个线程对象, 直接使用(将线程任务交给线程池完成), 线程对象可以反复使用
    newCachedThreadPool() : 根据需求提供线程
    newFixedThreadPool(int): 固定数量的线程
    newSingleThreadExecutor() : 提供一个线程
    newScheduledThreadPool() : 可以定时执行的线程

Callable / Runnable

