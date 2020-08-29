# kafka ansible脚本说明

由于文件大小限制，脚本中去除了jdk、kafka、zk等安装包。


## 集群安装方式：（files目录需要手动创建）

​	jdk安装包位置：roles\jdk\files

​    kafka安装包位置： roles\kafka\files

   kafka-manager-2.0.0.2.zip 文件位置： roles\kafka\files

   zk安装包位置：roles\zookeeper\files

注意安装包的版本需要与对应的task以及templates中的变量匹配

## 单节点安装方式：

  单节点安装jdk、kafka、zkkafka-manager-2.0.0.2.zip 文件位置都位于rpm包下
