---





---

# ServletRequest


\## 1.请求行    请求方式+URI

    获得请求的资源：

\- \`\`\`java
  String getRequestURI() -- 获取请求URI
  StringBuffer getRequestURL()
  String getQueryString() --获取get方式请求参数 结果例："name=wujie&pass=ling "
  \`\`\`

\## 2.请求头

\- \`\`\`java
  String getHeader(String name)
  long getDateHeader(String name)
  int getIntHeader(String name)
  Enumeration<String> getHeaderNames() 
  \`\`\`

\-  常见请求头

  1. User-Agent：浏览器告诉服务器，浏览器版本信息

     作用：解决浏览器的兼容性问题

  2. Referer：告诉服务器，请求从哪里来

     作用：防盗链

     盗链：获取别人的资源地址，绕过别人的资源展示页面，直接在自己的页面上向最终用户提供此内容

     处理方式：通过Referer截取域名判断是否时是自己的域名，不是可以重定向自己的页面

\## 3.请求体 (POST请求才有请求体)

1\. 获取流对象

2\. 从流对象拿取数据

\## 4.其他功能

1\. 获取请求参数

   \`\`\`java
   String getParameter(String name)
   String\[\] getParameterValues(String name) 参数名获取参数值的数组
   Enumeration<String> getParameterNames() 所有请求的参数名称
   Map<String,String\[\]> getParameterMap() 所有参数的map集合
   \`\`\`

        <mark style="background:lightblue">中文乱码问题</mark>

            get方式：tomcat 8将get编码默认设置为utf-8，解决中文乱码

            post：ISO8859-1编码，会乱码

                解决：在获取参数之前设置request.setCharacterEncoding("utf-8");

2\. 请求转发

   1. 获得转发器对象

      \`\`\`java
      request.getRequestDispatcher(路径); //此路径不需要应用名
      \`\`\`

   2. 使用RequesDispatcher对象来进行转发

      \`\`\`java
      request.getRequestDispatcher(路径).forword(ServletRequest request,
      ServletResponse response);      
      \`\`\`

         - 特点

         1.浏览器地址栏路径不发生变化

         2.只能转发到当前服务器内部资源中

         3.转发是一次请求

3\. 共享数据

   作为域对象

   方法：

       1.void setAttribute(String name,Object obj) 存储数据

       2.Object getAttribute(String name) 通过键获取值

       3.void removeAttribute(String name) 通过键移除键值对

           \*\*范围(根据生命周期)\*\*

               ServletContext

                   创建：服务器启动

                   销毁：服务器关闭

                   域的作用范围：整个web应用

               request

                   创建：访问时创建request

                   销毁：响应结束request销毁

                   域的作用范围：一次请求中

