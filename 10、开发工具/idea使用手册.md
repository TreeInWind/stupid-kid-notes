### 设置忽略文件

> 背景：idea commit 时总会带有非理想文件，比如.iml .idea文件，target 文件夹

解决办法：在 idea 中做相关配置，配置 setting 路径：搜索 file type，选中 file type类型，再右侧页面中配置需要忽略的文件类型和文件夹

<img src="./static/idea 设置忽略文件类型和文件夹.png" alt="idea 设置忽略文件类型和文件夹" style="zoom: 50%;" />

**示例：**

*.iml; -> 忽略所有iml类型的文件。

target	表示忽略文件夹名称为 target 的文件夹。 