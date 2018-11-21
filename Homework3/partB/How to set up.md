# How to set up?
## 下载压缩包
[zookeeper-3.4.12.tar.gz](https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/stable/zookeeper-3.4.12.tar.gz)

[kafka_2.12-2.0.1.tgz](http://mirror.bit.edu.cn/apache/kafka/2.0.1/kafka_2.12-2.0.1.tgz)


解压到本地目录

## 设置环境变量
- 设置系统变量ZOOKEEPER_HOME=(zookeeper解压目录)
- 编辑path系统变量，添加路径：%ZOOKEEPER_HOME%\bin

## 修改配置文件
- zookeeper
    - 将"zoo_sample.cfg"重命名为"zoo.cfg"
    - 打开"zoo.cfg"找到并编辑dataDir=(zookeeper解压目录)\tmp

- kafka
    - 进入config目录找到文件server.properties并打开
    - 找到并编辑log.dirs=D:\Kafka\kafka_2.12-0.11.0.0\kafka-logs
    - 找到并编辑zookeeper.connect=localhost:2181

## 运行
- 打开cmd，进入zookeeper目录输入“zkServer“，运行Zookeeper
- 打开新的cmd，进入kafka目录输入.\bin\windows\kafka-server-start.bat .\config\server.properties
- 打开新的cmd，进入kafka目录，输入.\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test，创建主题
- 输入.\bin\windows\kafka-topics.bat --list --zookeeper localhost:2181查看主题输入
- 输入.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic test创建生产者
- 打开新的cmd，输入.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning，创建消费者

## 参考文献
[在Windows安装运行Kafka](https://www.cnblogs.com/flower1990/p/7466882.html)
