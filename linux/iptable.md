
# CentOS6系统防火墙开启、关闭、查看状态

* 关闭防火墙：

	关闭命令：service iptables stop

	永久关闭防火墙：chkconfig iptables off

* 查看防火墙关闭状态
	service iptables status

* 其他命令
	1. 关闭防火墙-----service iptables stop 
	2. 启动防火墙-----service iptables start 
	3. 重启防火墙-----service iptables restart 
	4. 查看防火墙状态--service iptables status 
	5. 永久关闭防火墙--chkconfig iptables off 
	6. 永久关闭后启用--chkconfig iptables on

* 注：centos 7 使用firewall

