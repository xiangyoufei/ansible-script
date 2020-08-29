mysql单节点部署： 

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
	[single-mysql]
	10.200.60.19
	备注：10.200.60.19为安装mysql单节点主机IP

三. 修改/ansible单节点部署/ansible-single-mysql/vars.yml文件
	mysql_path: /ansible-single-mysql/rpm
	root_password: gridsum1234
	备注：mysql_path为mysql.rpm的存放路径,root_password 为mysql的root用户密码。
  
四. 执行启动命令进行集群部署：
	cd /ansible单节点部署/ansible-single-mysql
    ansible-playbook install-mysql.yml            

