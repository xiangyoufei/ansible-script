redis集群自动化部署：

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
	
二. 修改/ansible-redis/hosts文件
	[redis]
	10.200.60.67   master=true
	10.200.60.39
	10.200.60.30

	[redis:vars]
	mport=7000
	sport=7001
	
	备注：根据具体的安装redis的主机IP进行修改。

三. 修改/ansible-redis/group_vars/redis.yml文件	
	---
	redis_list:
	  - name: redis_master_info
		port: 7000
	  - name: redis_slave_info
		port: 7001

	redis_bin:
	  - redis-benchmark
	  - redis-check-aof
	  - redis-check-rdb
	  - redis-trib.rb
	  - redis-cli
	  - redis-sentinel
	  - redis-server


	redis_cluster_ip:
	 - 10.200.60.67
	 - 10.200.60.39
	 - 10.200.60.30
	
	 备注：redis_cluster_ip:为安装redis集群的主机IP。
	 
四. 执行脚本
	cd /ansible-redis/
	ansible-playbook  -i hosts -t remove_dir site.yml
  	ansible-playbook  -i hosts site.yml










