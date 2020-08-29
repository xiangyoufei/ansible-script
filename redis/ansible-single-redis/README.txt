redis单节点自动化部署：

一.  ansible免密操作
    在ansible主机执行
    cd /root/.ssh
    ssh-keygen -t rsa   #一直回车完成
	在ansible主机上将所要部署所有目标主机进行如下操作
    ssh-copy-id -i /root/.ssh/id_rsa.pub root@目标主机IP
	输入登录密码
	执行下面命令进行验证
	ssh root@目标主机IP
	
二. 修改/etc/ansible/hosts文件
    [single-redis]
	10.200.60.19
	备注：10.200.60.19为安装redis单节点的主机IP

三. 修改/ansible单节点部署/ansible-single-redis/vars.yml文件	
	port: 6379
	redis_bin_path: /ansible-single-redis/files
	redis_bin:
	  - redis-benchmark
	  - redis-check-aof
	  - redis-check-rdb
	  - redis-trib.rb
	  - redis-cli
	  - redis-sentinel
	  - redis-server
	 备注：redis_bin_path为redis_bin的存放路径，根据具体情况进行修改。
	 
四. 执行脚本
	cd /ansible单节点部署/ansible-single-redis
	ansible-playbook  install-redis.yml










