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
	例如：
	追加
	[single-rabbitmq]
	10.200.60.12
    备注：10.200.60.12为安装rabbitmq的单节点ip

三. 修改/ansible单节点部署/ansible-single-rabbitmq/vars.yml文件

	erlang_url：erlang-21.3.8.2-1.el7.x86_64.rpm的全路径。例：/data/yum_data/soft/erlang-21.3.8.2-1.el7.x86_64.rpm
	socat_url：socat-1.7.3.2-2.el7.x86_64.rpm的全路径
	rabbitmq_url：rabbitmq-server-3.8.1-1.el7.noarch.rpm的全路径
	username：创建rabbitmq的用户。例：admin
	password：创建新用户的密码。例：admin

四. 执行脚本
	cd /ansible单节点部署/ansible-single-rabbitmq
	ansible-playbook install-rabbitmq.yml

