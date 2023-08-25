---





---

# Form表单接收数据


\### 文本框(text,email)date选择框接收

\- 存在参数但未填 -> ""

\- 不存在参数 -> null

\### 文件上传接收

\- 只能用POST方法

\- 表单 \*\*enctype\*\* 属性应该设置为 \*\*multipart/form-data\*\*，否则只有文件名

\### 多选框接收  (一个name对应多个值)

\- \`\`\`java
  String\[\] names = request.getParameterValues("name");
  \`\`\`

\- 不勾选值为null

\- 没有设置value值选中默认为on

\### 单选框接收

\- 不勾选则没有这个参数

\- 没有设置value值选中默认为on

\### 下拉列表接收

\- 没有value则为选项中的文本内容，有则为value值

