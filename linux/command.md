
# 常用命令

ls          查看目录  
cd          切换目录  
pwd         当前路径  
df -h       显示已经挂载的分区列表  

cat [file_name] 查看文本  
tac         倒过来的cat  
nl          带行号cat  
more        类cat 空格翻页回车下一行  
less more   支持详情翻页  
head [-n linenum] 只显示前几行  
tail        只看尾几行  S
od          二进制读取文件  
wc          统计文本中行数、字数、字符数  

find [dir] -name *[file_name]* 搜索文件  
grep -i [key] 文本搜索 (-i忽略大小写)  

rm          删除文件 (rm -rf r递归 f强制)  
cp [src] [dest] 复制  
mv          移动/改名  
mkdir       建立目录  
rmdir       删除目录  
touch       修改创建时间或新建文件  

man         帮助  

kill        杀进程
ps -ef      查看活动进程  
ps -aux     查看活动进程格式2  
top         查看cpu内存使用情况  

tab         自动补全  
tab tab     预览  
ctrl+c      结束当前程序  
ctrl+d      输入结束exit  

ctrl+z      当前程序切换到后台  
fg          后台进程调到前台  
jobs        查看后天进程  

chgrp       改变群组  
chown       改变拥有者  
chmod       改变权限  

cal         日历  
date        时间  
bc          计算器  

file        观察文件类型  
which       寻找执行档  
whereis     寻找特定档案  
locate      寻找特定档案  
who         显示在线登陆用户  
ifconfig    查看网络情况  
netstat     显示网络状态信息  
clear       清屏  

basename [path] 文件名  
dirname [path] 目录名  

reboot      重启  
shutdown    关机
