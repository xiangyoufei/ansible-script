kafka集群部署：至少准备三台机器

一.  ansible免密操作
    在ansible主机执行
    cd /root/.ssh
    ssh-keygen -t rsa   #一直回车完成
	在ansible主机上将所要部署所有目标主机进行如下操作
    ssh-copy-id -i /root/.ssh/id_rsa.pub root@目标主机IP
	输入登录密码
	执行下面命令进行验证
	ssh root@目标主机IP
	看是否能够切换到目标主机，如果可以说明免密操作成功，使用exit进行退出，其余同上。

二. 修改/ansible-kafka/hosts文件：
	例如：
	[kafka]
	10.200.60.27 hostname=kafka1 myid=1 broker_id=1  master=true
	10.200.60.72 hostname=kafka2 myid=2 broker_id=2
	10.200.60.61 hostname=kafka3 myid=3 broker_id=3
   
   ​	备注： ip以及hostname根据主机进行配置， myid、broker_id 保证唯一性可以不进行修改。
   
三. 修改/ansible-kafka/roles/common/vars/main.yml文件
	例如：
	host_list:
	 - ip: 10.200.60.27
	   name: kafka1
	 - ip: 10.200.60.72
	   name: kafka2
	 - ip: 10.200.60.61
	   name: kafka3
    备注：ip和name需要一一匹配。
	
四. 修改/ansible-kafka/roles/zookeeper/vars/main.yml 文件
	例如：
	server1_hostname: kafka1
	server2_hostname: kafka2
	server3_hostname: kafka3
	file_dir:
	  - DataDir
	  - DataLogDir
	备注：根据具体情况有几个添加几个，主机名称要统一。
	
五. 修改/ansible-kafka/roles/zookeeper/templates/zoo.cfg.j2文件
	例如：
	server.1={{ server1_hostname }}:2888:3888
	server.2={{ server2_hostname }}:2888:3888
	server.3={{ server3_hostname }}:2888:3888
	备注：根据第五步操作有几个kafka就添加几个。
	
六. 修改/ansible-kafka/roles/kafka/vars/main.yml文件
	例如：
	zk_cluster: 10.200.60.27:2181,10.200.60.72:2181,10.200.60.61:2181
	备注：根据所配置的kafka主机数量对其进行修改。
	
七. 执行方式：
	cd /ansible-kafka
  	ansible-playbook  -i hosts -t remove_dir site.yml
  	ansible-playbook  -i hosts site.yml



