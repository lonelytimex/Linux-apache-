Linux搭建apache服务
安装依赖：yum install gcc-c++ zlib-devel openssl-devel
安装apr
[root@localhost ~]# tar zxf apr-1.5.2.tar.gz
[root@localhost ~]# cd apr-1.5.2/
[root@localhost apr-1.5.2]# ./configure --prefix=/usr/local/apr
[root@localhost apr-1.5.2]# make && make install

安装apr-util
[root@localhost ~]# tar zxf apr-util-1.5.4.tar.gz 
[root@localhost ~]# cd apr-util-1.5.4/
[root@localhost apr-util-1.5.4]# ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr
[root@localhost apr-util-1.5.4]# make && make install

安装pcre
[root@localhost ~]# tar zxf pcre-8.40.tar.gz
[root@localhost ~]# cd pcre-8.40/
[root@localhost pcre-8.40]# ./configure --prefix=/usr/local/pcre
[root@localhost pcre-8.40]# make && make install

安装httpd
[root@localhost ~]# tar zxf httpd-2.4.25.tar.gz
[root@localhost ~]# cd httpd-2.4.25/
[root@localhost httpd-2.4.25]# ./configure --prefix=/usr/local/apache --sysconfdir=/etc/httpd --enable-so --enable-ssl --enable-cgi --enable-rewrite --enable-zlib --enable-modules=most --enable-mpms-shared=all --with-mpm=prefork --with-apr=/usr/local/apr --with-apr-util=/usr/local/apr-util --with-pcre=/usr/local/pcre
[root@localhost httpd-2.4.25]# make && make install
设置防火墙
[root@localhost ~]# firewall-cmd --permanent --add-service=http
[root@localhost ~]# firewall-cmd --reload
[root@localhost ~]# setenforce 0
[root@localhost ~]# ln -s /usr/local/apache/bin/* /usr/sbin/
启动httpd
[root@localhost ~]# httpd -k start
查看80端口是否启用
[root@localhost ~]# netstat -anlpt | grep httpd
复制启动脚本
[root@localhost ~]# cp /usr/local/apache/bin/apachectl /etc/init.d/httpd
编辑开机自动启动
[root@localhost ~]# vim /etc/init.d/httpd
在配置文件中加入：chkconfig:35 87 30
[root@localhost ~]# chkconfig --add httpd
[root@localhost ~]# chkconfig httpd on

输入IP地址访问出现It works!就安装成功了






