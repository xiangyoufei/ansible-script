kafka单节点部署：

一.  ansible免密操作
    在ansible主机执行
    cd /root/.ssh
    ssh-keygen -t rsa   #一直回车完成
	在ansible主机上将所要部署所有目标主机进行如下操作
    ssh-copy-id -i /root/.ssh/id_rsa.pub root@目标主机IP
	输入登录密码
	执行下面命令进行验证
	ssh root@目标主机IP

二. 修改/etc/ansible/hosts文件：
	例如：
	[single-kafka]
	10.200.60.13
	
	备注：根据具体的ip地址进行修改。
	
三. 修改/ansible单节点部署/ansible-single-kafka/vars.yml文件
	例如：
	ip: 10.200.60.13
	name: kafka1
	server1_hostname: kafka1
	file_dir:
	  - DataDir
	  - DataLogDir
	zk_cluster: 10.200.60.13:2181
	jdk_package_name: jdk-8u181-linux-x64.rpm
	jdk_path: /ansible-single部署/rpm/jdk-8u181-linux-x64.rpm
	zk_path: /ansible-single部署/rpm/apache-zookeeper-3.5.6-bin.tar.gz
	zoo.cfg_path: /ansible-single部署/zoo.cfg.j2
	zk_bin_name: apache-zookeeper-3.5.6-bin
	kafka_path: /ansible-single部署/rpm/kafka_2.13-2.4.0.tgz
	server.properties_path: /ansible-single部署/server.properties.j2
	kafka_edition: kafka_2.13-2.4.0
	myid: 1
	broker_id: 1

	备注：ip为安kafka的主机ip，name为安装kafka的主机名，zk_cluster为安装Zookeeper的主机和端口号
	，jdk_package_name为jdk.rpm包名，jdk_path为jdk.rpm的存放路径,zk_path为zk的存放路径，zoo.cfg_path为zoo.cfg.j2的存放路径，
	zk_bin_name为目录名，具体情况具体命名，kafka_path为kafka的存放路径，server.properties_path为server.properties.j2的存放路径，。kafka_edition为目录名，具体情况具体命名。
	
四. 执行方式：
	cd  /ansible单节点部署/ansible-single-kafka
  	ansible-playbook  install-kafka.yml
 


