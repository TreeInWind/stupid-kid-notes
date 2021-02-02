### 使用docker拉取镜像

* docker search pulsar：搜索出来相关内容

  ~~~powershell
  ### 搜索结果如下
  NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
  apachepulsar/pulsar               Apache Pulsar - Distributed pub/sub messagin…   31                                      
  apachepulsar/pulsar-all                                                           10                                      
  apachepulsar/pulsar-standalone                                                    5                                       
  apachepulsar/pulsar-dashboard                                                     3                                       
  streamlio/pulsar                  Apache Pulsar - Distributed pub/sub messagin…   3                                       
  kafkaesqueio/pulsar-all           Apache Pulsar with all optional packages inc…   2                                       
  streamnative/pulsar-manager       A pulsar manager to manage Apache Pulsar clu…   2                                       
  apachepulsar/pulsar-grafana                                                       1                                       
  streamnative/pulsar                                                               1                                       
  apachepulsar/pulsar-build         Docker image used for Pulsar CI builds.         1                                       
  apachepulsar/pulsar-manager                                                       1                                       
  streamnative/pulsar-all                                                           1                                       
  hsldevcom/pulsar-mqtt-gateway     https://github.com/HSLdevcom/pulsar-mqtt-gat…   0                                       
  quinovas/pulsar-perf-test         Performance testing for pulsar using python …   0                                       
  quinovas/pulsar                   Apache Pulsar Broker                            0                                       
  pulsarsmarthome/pulsarpi          Pulsar Raspberry Pi Release                     0                                       
  kafkaesqueio/pulsar               Apache Pulsar                                   0                                       
  galaxy/pulsar                     Container for running Pulsar's test suite.      0                                       [OK]
  andrewgrange/pulsar               Pulsar docker image                             0                                       
  skybig/pulsar-operator            pulsar operator creates/configures/manages p…   0                                       
  nsingla/pulsar-client-go-test                                                     0                                       
  kafkaesqueio/pulsar-beam                                                          0                                       
  saandrews/pulsar                                                                  0                                       
  kafkaesqueio/pulsar-ops-monitor                                                   0                                       
  bbonnin/pulsar-express                                                            0       
  
  ~~~

* docker pull apachepulsar/pulsar：找到需要的那款无情拉取

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
  docker run -it -p 6650:6650 -p 6651:8080 --name pulsar --restart=always -d --net app --ip 172.16.1.7 --mount source=pulsardata,target=/docker/pulsar/data --mount source=pulsarconf,target=/docker/pulsar/conf apachepulsar/pulsar:latest bin/pulsar standalone
  
  ### 命令解析
  $ docker run -it 
    -p 6650:6650 
    -p 6651:8080
    --name pulsar 容器命名
    --restart=always -d 随docker的启动而自启动
    --net app --ip 172.16.1.7 定义内部通信地址
    --mount source=pulsardata,target=/docker/pulsar/data 定义挂载数据目录
    --mount source=pulsarconf,target=/docker/pulsar/conf 定义配置文件目录
    apachepulsar/pulsar:2.7.0 
    bin/pulsar standalone
    
    
  
  
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