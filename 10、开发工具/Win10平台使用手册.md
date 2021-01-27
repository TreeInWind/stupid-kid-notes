#### 修改host文件

* host文件目录位置：

  win10：C:\Windows\System32\drivers\etc

* 修改文件方法：

  获取管理员权限：

  1、邮件点击属性再安全tab下修改当前用户权限

  2、使用notepad++打开编辑，保存时notepad++会提示是否使用管理员权限编辑

  <img src=".\static\host文件修改示例.png" alt="host文件修改示例" style="zoom: 50%;" />

* 测试所做修改是否生效：

  在控制台中，使用ping ip查看是否有字节可传输

<img src=".\static\host文件修改测试示例.png" alt="host文件修改示例" style="zoom: 50%;" />

* 不生效的解决办法：

  可能是本地DNS缓存导致的，ipconfig /flushdns 命令手动刷新缓存，然后测试