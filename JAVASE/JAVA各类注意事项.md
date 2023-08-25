---





---

# JAVA各类注意事项


1.static
		static方法可被继承，子类中有相同的static方法父类的static方法会被隐藏。
![[./_resources/JAVA各类注意事项.resources/msedge_7toh9YTQp7.png]]![[./_resources/JAVA各类注意事项.resources/msedge_JZnFAs9Qmy.png]]

2.权限控制: 访问修饰词
                自己类中    同包中    父子类    工程中
  public          √        √        √        √
  protected    √        √        √
  friendly        √        √
  private          √

