进入Linux服务器 默认使用centos6.5做示例
一、
1. yum install tinyproxy
配置
2.vim /etc/tinyproxy/tinyproxy.conf
             修改Port 端口号为你想设定的值
             将Allow 选项后面的IP改成你想使用这个代理的客户机的IP，如果你想任何人都可以访问，把这行前面加个#注释一下就行了
             使用
3.service tinyproxy start 
                service tinyproxy stop
                service tinyproxy restart
	来停止、启动、重启tinystart
	将tinyproxy设置开机启动
4.chkconfig --level 2345 tinyproxy on
设置防火墙
5. iptables -I INPUT -p tcp --dport 8888 -j ACCEPT  && service iptables save &&service iptables restart
默认的进程端口是8888如果修改了命令要替换

6.配置服务器的安全组规则

二、
当遇到
http://mirrors.aliyun.com/centos/6/os/x86_64/repodata/repomd.xml: [Errno 14] PYCURL ERROR 22 - "The requested URL returned error: 404 Not Found" Trying other mirror.
http://mirrors.aliyuncs.com/centos/6/os/x86_64/repodata/repomd.xml: [Errno 14] PYCURL ERROR 7 - "couldn't connect to host" Trying other mirror.
Error: Cannot retrieve repository metadata (repomd.xml) for repository: base. Please verify its path and try again
报错时需要重新指定yum得镜像地址
1.   cd /etc/yum.repos.d/
2.   echo "" >  CentOS-Base.repo
3.   echo "" >  epel.repo
先清空这两个文件的内容
4.  vim  CentOS-Base.repo 
进入编辑文件按大写i进行编辑，文件内容地址参考https://www.jianshu.com/p/4d5e5360c55b 复制进去后按 : wq 进行保存
5. vim epel.repo 
同理
6.  wget -O /etc/yum.repos.d/CentOS-Base.repo http://file.kangle.odata.cc/repo/Centos-6.repo
7.  wget -O /etc/yum.repos.d/epel.repo http://file.kangle.odata.cc/repo/epel-6.repo
8.  yum clean all
9.  yum makecache
再继续执行上方的命令



