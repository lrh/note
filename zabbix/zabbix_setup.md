
# Centos 7安装部署zabbix3.0实战（服务器端）

## 一、服务器端部署

### 1、Zabbix 环境准备

```bash
[root@localhost]#hostnamectl set-hostname zabbix    #永久修改主机名

[root@zabbix ~]# cat /etc/redhat-release      # 查看系统版本

# > CentOS Linux release 7.2.1511 (Core)

[root@zabbix ~]# uname -r                # 查看内核版本

# > 3.10.0-327.18.2.el7.x86_64

[root@zabbix ~]# vi  /etc/sysconfig/selinux    #关闭selinux重启才会生效

# > SELINUX=disabled

[root@zabbix ~]# setfenforce 0                    #设置临时关闭selinux

[root@zabbix ~]# systemctl stop firewalld     # 关闭 firewall 防火墙

[root@zabbix ~]# ifconfig eth0 | awk -F ‘[ :]+’‘NR==2{print $4}’      # 查看 IP 地址

# > 10.16.3.252
```

### 2、Zabbix 安装

Zabbix 存储配置包以及 yum 配置文件

<http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm>

```bash
[root@zabbix ~]# rpm -ivh http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm

[root@zabbix ~]# yum install -yzabbix-server-mysql zabbix-web-mysql zabbix-agent  mariadb-server
```

### 3、 初始数据库

创建 Zabbix 数据库以及用户授权
```bash
[root@zabbix ~]#systemctl start mariadb         #开启mariadb

[root@zabbix ~]#systemctl enable mariadb      #加入开机自启动

[root@zabbix ~]# mysql -uroot -p

MariaDB [(none)]> create database zabbix character set utf8 collateutf8_bin;

# > Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> grant all privileges on zabbix.* to zabbix@localhostidentified by ‘zabbix’;   //授权

# > Query OK, 0 rows affected (0.00 sec)
```

导入初始模式和数据
```bash
[root@zabbix ~]# cd /usr/share/doc/zabbix-server-mysql-3.0.3/

[root@zabbix zabbix-server-mysql-3.0.3]# zcat create.sql.gz | mysql -urootzabbix
```

### 4、 启动Zabbix 服务器进程

编辑数据库配置
```bash
[root@zabbix ~]# grep  ^[a-Z]  /etc/zabbix/zabbix_server.conf

LogFile=/var/log/zabbix/zabbix_server.log

LogFileSize=0

PidFile=/var/run/zabbix/zabbix_server.pid

DBHost=localhost

ListenIP=localhost           #数据库ip地址

DBName=zabbix

DBUser=zabbix

DBPassword=zabbix

SNMPTrapperFile=/var/log/snmptrap/snmptrap.log

Timeout=4

AlertScriptsPath=/usr/lib/zabbix/alertscripts

ExternalScripts=/usr/lib/zabbix/externalscripts

LogSlowQueries=3000
```

启动 Zabbix 服务器进程
```bash
[root@zabbix ~]#  systemctl start zabbix-server

[root@zabbix ~]#  systemctl enable  zabbix-server
```

启动 Zabbix 客户端进程
```bash
[root@zabbix ~]#  systemctl start zabbix-agent

[root@zabbix ~]#  systemctl enable zabbix-agent
```

### 5、 编辑 Zabbix 前端 PHP 配置

Apache 的配置文件 /etc/httpd/conf.d/zabbix.conf 一些 PHP 设置已经配置好了。取消注释，设置正确的时区
```bash
[root@zabbix ~]# vim /etc/httpd/conf.d/zabbix.conf

php_value max_execution_time 300

php_value memory_limit 128M

php_value post_max_size 16M

php_value upload_max_filesize 2M

php_value max_input_time 300

php_value always_populate_raw_post_data -1

php_value date.timezone Asia/Shanghai
```

启动 ApacheWeb 服务器
```bash
[root@zabbix ~]# systemctl start httpd

[root@zabbix ~]# systemctl enable  httpd
```

## 二、安装 Zabbix Web

浏览器访问网址 <http://10.16.3.252/zabbix>

 web 安装向导的第一个屏幕

wKioL1f5rlzwjKYFAABGWqfqb4U388.png-wh_50

确保所有软件先决条件都是OK才可以

输入连接到数据库详细信息，密码要自己设置wKioL1f5rtuQbwp-AACP569QQ5w653.png-wh_50

连接 Zabbix 服务细节，如果没有改变可选择默认

回顾一个设置概要

完成安装，会在 /etc/zabbix/web/zabbix.conf.php 生成配置文件

Zabbix 登陆准备。 默认的用户名 / 密码为 Admin / zabbix

## 三、Zabbix服务器监控自己配置

zabbix服务器要监控自己，也要安装客户端包zabbix-agent
``` bash
# yum -y install zabbix-agent              //上面已经安装了，这里就不用安装了，勿略这步

# vi /etc/zabbix/zabbix_agentd.conf                  //修改zabbix_agentd.conf参数

Hostname=Zabbix                        //在本机上用hostname查看的结果必须和服务端添加的相同

Server=10.16.3.252,127.0.0.1                //zabbix服务器的ip

LogFile=/var/log/zabbix/zabbix_agentd.log       //本机agentd日志保存文件

SourceIP=10.16.3.252            //本机IP

ListenPort=10050
```
修改/etc/services增加服务端口，添加下面的内容：
```bash
zabbix-agent    10050/tcp Zabbix Agent

zabbix-agent    10050/udp Zabbix Agent

zabbix-trapper  10051/tcp Zabbix Trapper

zabbix-trapper  10051/udp Zabbix Trappe
```

重启服务： sysytemctl restart zabbix-agent
