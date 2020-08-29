mysql集群部署： 

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
二. 修改/ansible-mysql/hosts文件
	  [mysql]
	   10.200.60.17  server_id=100 master=true
	   10.200.60.37  server_id=200
	   10.200.60.12  server_id=300
	备注：具体情况具体修改。

三. 修改/ansible-mysql/group_vars/mysql.yml文件
	group_seeds: mysql1:33306,mysql2:33306,mysql3:33306
	root_password: gridsum1234
	备注：root_password 为mysql的root用户密码，mysql1为安装mysql的主机名。
  
四. 执行启动命令进行集群部署：
	cd /ansible-mysql
    ansible-playbook  -i hosts -t remove_dir site.yml
    ansible-playbook  -i hosts site.yml

