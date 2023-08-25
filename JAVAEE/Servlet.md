---





---

# Servlet


Java接收http请求-->Servlet: Server + Applet
请求url:  http://localhost:8080/web01/form.html
                        tomcat/应用名/资源
                        tomcat/应用名(访问首页index)

动态资源: 由Java编写, 并且可以接收请求的一个class类,能接受请求的java类, 符合JavaEE规范 -> servlet jsp

### Servlet规范: 3个接口  第一个接口: Servlet

实现Servlet步骤:

1.  自定义类 实现 Servlet接口
2.  注册servlet -> web.xml

		     <servlet>
		         <servlet-name>demo1</servlet-name>
		         <servlet-class>全限定类名</servlet-class>
		     </servlet>
		     <servlet-mapping>
		         <servlet-name>demo1</servlet-name>
		         <url-pattern>/hello</url-pattern>
		     </servlet-mapping>

### 测试Servlet生命周期:

   init: 对象初始化时调用
		对象是在创建后初始化
		对象默认第一次访问资源时创建
		可以通过标签 <load-on-startup>int 来修改为服务器启动时创建
   destroy: 对象销毁前调用
		服务器关闭之前销毁
   service: servlet接收到请求时调用
   结论: 在整个服务器(应用)运行期间, Servlet 是单例的

注意:
    服务器启动：应用的安装和启动        
    服务器关闭：应用的卸载和关闭

### HttpServlet类

Servlet -> HttpServlet extends GenericServlet
implements Servlet
   1. HttpServlet 间接实现了 Servlet 接口
   2. 实现了Servlet接口中的service方法
      将请求和响应做了类型转换后, 调用了 this.service 方法
   3. this.service 方法中
      如果请求方式是get:  调用doGet方法
      如果请求方式是Post: 调用doPost方法
   4. 重写 doGet 或者 doPost

### servlet的路径配置

  1.一个servlet可以匹配多个url-pattern
  2.url-pattern写法:
     1.完全匹配的写法, 怎么写的怎么访问
		    <url-pattern>/user/demo2</url-pattern> -> 优先级最高
    2.目录匹配的写法, 有(没有)目录作为统一前缀, 后面使用通配符 \*
		    <url-pattern>/user/\*</url-pattern> -> 优先级第二
    3.后缀匹配的写法, 有统一后缀, 前面使用通配符 \*
		    注意: 后缀匹配, 前面不能用目录, 不能用 / -->
		    <url-pattern>\*.do</url-pattern> -> 优先级第三, 高于静态资源
		     不推荐后缀是常见文件后缀    .user .admin .do .action
   4.默认(缺省)的配置    /     了解什么是DefaultServlet  (一般不修改)
		    <url-pattern>/</url-pattern> -> 最四优先级, 高于静态资源
				默认的配置: 当在web.xml里面找不到任何映射的资源时, 就会去访问default配置 /
				静态资源, 不是直接找文件, 也是在web应用中找路径对应的Servlet映射
				在发送请求时, tomcat 解析url路径(访问的是哪个应用), 后面的路径是访问的资源
				路径搜索有没有对应的映射, 自己应用中的描述文件web.xml, tomcat的描述文件web.xml
				tomcat的web.xml文件中定义了默认的DefaultServlet, 可以处理所有的静态资源
    5.web3.5版本以上, 就支持注解配置
		    @WebServlet(name="Demo4Servlet", urlPatterns = {"/demo4", "/hi/demo4"},
		            loadOnStartup = 2)

### ServletConfig对象: Servlet配置对象

获得servlet的初始化参数(注册servlet的时候配置的)
    init(): Servlet对象初始化时, tomcat负责传递进来的
    配参数:  web.xml文件中
    例
    <servlet>
       <init-param>
           <param-name>driver</param-name>
           <param-value>com.mysql.cj.jdbc.Driver</param-value>
       </init-param>
    </servlet>

### ServletContext: 应用上下文, 一个应用中只有一个的

		生命周期: 应用运行期间只有一个
		创建: 开启服务器创建
		销毁: 关闭服务器销毁
		

```
package c_context;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
@WebServlet("/context")
public class DemoContextServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 获得ServletContext
        // 方式1: 通过ServletConfig获得
        // 方式2: 通过request获得
        ServletContext context = request.getServletContext();
        // 方式3: 通过Servlet获得
        ServletContext application = this.getServletContext();
        System.out.println(application == context);

        // 所有的基础功能都和get相关
        // 功能1: 可以动态获得应用名 - 应用名因为可能随时变, 所以不要写在代码中
        String path = application.getContextPath();
        response.getWriter().println("path: " + path);

        // 功能2: 可以获得应用的初始化参数<context-param> -> 只能写在web.xml
        String password = application.getInitParameter("password");
        response.getWriter().println("password: " + password);

        // 功能3: ☆☆☆☆☆获得应用中资源的绝对路径
        // a.txt -> web工程/src/a.txt
        // b.txt -> web工程/web/b.txt
        // c.txt -> web工程/web/WEB-INF/c.txt
        // d.txt -> web工程/d.txt -> 不会出现在应用中
        String aPath = application.getRealPath("WEB-INF/classes/a.txt");
        String bPath = application.getRealPath("b.txt");
        String cPath = application.getRealPath("WEB-INF/c.txt");
        response.getWriter().println("a: " + aPath);
        response.getWriter().println("b: " + bPath);
        response.getWriter().println("c: " + cPath);

        // 功能4 域对象
        // 域对象：存储数据，取出数据，范围取决与对象的生命周期
        // Object setAttribute(key,value)
        // Object getAttribute(Key)
        // void removeAttribute(Key)

        // 向context中存数据
        context.setAttribute("name", "zhangsan");     
        // 从context中取数据 -> 需要确定类型
        String name = (String) application.getAttribute("name");
        // 从context中删除数据
        application=.removeAttribute("name");   
    }
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}
```

