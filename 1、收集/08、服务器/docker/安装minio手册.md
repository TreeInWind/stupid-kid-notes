### 使用docker拉取镜像

* docker search minio：搜索出来相关内容

  ~~~powershell
  ### 搜索结果如下
  NAME                           DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
  minio/minio                    Minio is an Amazon S3 compatible object stor…   371                                     [OK]
  minio/mc                       Minio Client (mc) provides a modern alternat…   18                                      [OK]
  jessestuart/minio              Minio server — supports arm (arm32v6, arm32v…   5                                       
  pixelchrome/minio-arm          This Dockerfile installs Minio on your ARM-P…   4                                       
  webhippie/minio                Docker images for Minio                         3                                       [OK]
  bitnami/minio                  Bitnami MinIO Docker Image                      3                                       
  opennms/minion                 Application container runs Minion by OpenNMS…   3                                       [OK]
  ~~~

* docker pull minio/minio：找到需要的那款无情拉取

  * 类似git中的pull

  ~~~shell
  ### 拉取完控制台的展示结果（过程中会有进度条标识拉取进度的东西，你一看就明白）
  Using default tag: latest
  latest: Pulling from minio/minio
  df20fa9351a1: Pull complete 
  0eb214a82c49: Pull complete 
  Digest: sha256:3d9a4597d1d7b80d29bfe957f78e51be8bce731bf3869165a6ecf4c42ad7f166
  Status: Downloaded newer image for minio/minio:latest
  docker.io/minio/minio:latest
  
  ~~~

  

### 启动镜像

> 此时，你已经把镜像拉取到docker中啦，接下来要把镜像启动

* 首次启动

  ~~~shell
  ### 启动命令
  docker run -p 9000:9000 --name gold_minio --restart=always -d --net app --ip 172.16.1.4  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE"   -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"   
  -v /docker/nginx/html/data:/data   
  -v /docker/minio/config:/root/.minio   minio/minio server /data
  
  ### 文件挂载目录 /docker/nginx/html/data
  
  ### systemctl status docker  -l
  查看docker中内网镜像的内网地址
  
  ### 命令解析
  --name gold_minio 给启动的容器指定一个名字
  --restart=always 设置容器跟随docker的重启而重启
  -d 后台执行
  --net app --ip 172.16.1.4 设置同服务器中容器间通信IP
  /docker/minio/data:/data 指定data目录，也就是我们后续上传文件的位置
  /docker/minio/config:/root/.minio 指定的配置文件的位置
  
  ### 启动成功的响应展示结果
  4b257271dacba909bc74abf271a5b2af178c33152a62dea66c119475e3bfcade
  
  ~~~

* 非首次启动

  ~~~shell
  ### 根据模糊ID启动指定容器
  docker start <container_id>
  
  ### 对应的关闭容器命令
  docker stop <container_id>
  ~~~

### 检查是否启动成功

* 到浏览器登录 Ip:port ，进入到登录页面，输入账户名和密码（就是我们docker run时设置的MINIO_ACCESS_KEY和MINIO_SECRET_KEY）

### 查看minio的MINIO_ACCESS_KEY和MINIO_SECRET_KEY

* 很遗憾，暂时没有找到。。。待续





1、开发处理文件的接口
2、调整minio服务器上传文件找那个镜像之间的通信，定义的内网地址：172.16.1.4



docker run -p 9000:9000 --name gold_minio --restart=always -d --net app --ip 172.16.1.4  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE"   -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"   -v /docker/minio/data:/data   -v /docker/minio/config:/root/.minio   minio/minio server /data