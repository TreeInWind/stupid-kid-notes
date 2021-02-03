## 系统使用

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



### 修改win下键位映射

> 参见几篇详细的博客手册

### 快捷键使用

win + d 快速切换到桌面



| 快捷键   | 作用                          | 备注 |
| -------- | ----------------------------- | ---- |
| win + d  | 快速回到桌面                  |      |
| F11      | 全屏当前页面/退出当前页面全屏 |      |
| Ctrl + d | 删除选中的文件                |      |
|          |                               |      |
|          |                               |      |
|          |                               |      |
|          |                               |      |
|          |                               |      |





## 软件使用

### cmder

> 一款可替代系统自带 **cmd** 控制台的交互软件

* 切换盘符：

  此时使用 cd C: 是不生效的，切换盘符直接 C: 即可，实战经验告诉我就是这样

* 修改默认目录：

  <img src="./static/cmder修改默认开启目录.png" />

     



### 修改键盘对应键的映射关系

https://blog.csdn.net/qq_15210067/article/details/78260391