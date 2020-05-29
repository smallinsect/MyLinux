# MyLinux

## 命令笔记

```
查看包含“server”的进程
ps -aux | grep server
USER    进程所属用户
PID     进程ID
%CPU    进程占用CPU百分比
%MEM    进程占用内存百分比
VSZ     虚拟内存占用大小   单位：kb（killobytes）
RSS     实际内存占用大小   单位：kb（killobytes）
TTY     终端类型
STAT    进程状态
START   进程启动时刻
TIME    进程运行时长
COMMAND 启动进程的命令

查看包含“server”的id进程
ps -ef | grep server

查看进程占用端口
netstat -nap|grep 20696
netstat -nap|grep mongod

创建文件夹
mkdir 文件名

杀掉进程
kill -9 pid

查看内存信息
free -h


```

# Linux修改环境变量

方法一：

```
在/etc/profile文件中添加变量【对所有用户生效(永久的)】
用VI在文件/etc/profile文件中增加变量，该变量将会对[Linux](http://www.chinabyte.com/keyword/Linux/)下所有用户有效，并且是“永久的”。
要让刚才的修改马上生效，需要执行以下代码
# source /etc/profile
```

方法二：

```
在用户目录下的.bash_profile文件中增加变量【对单一用户生效(永久的)】
用VI在用户目录下的.bash_profile文件中增加变量，改变量仅会对当前用户有效，并且是“永久的”。
要让刚才的修改马上生效，需要在用户目录下执行以下代码
# source .bash_profile
```

方法三：

```
直接运行export命令定义变量【只对当前shell(BASH)有效(临时的)】
在shell的命令行下直接使用[export变量名=变量值]定义变量，该变量只在当前的shell(BASH)或其子shell(BASH)下是有效的，shell关闭了，变量也就失效了，再打开新shell时就没有这个变量，需要使用的话还需要重新定义。
例如：export PATH=/usr/local/webserver/php/bin:$PATH
```

# Linux防火墙

```
#停止firewall
systemctl stop firewalld.service 
#开启firewall
systemctl start firewalld.service
#禁止firewall开机启动
systemctl disable firewalld.service 
#查看默认防火墙状态（关闭后显示not running，开启后显示running）
firewall-cmd --state
```

# Shell命令

## 学习网址
- https://www.runoob.com/linux/linux-shell.html

## 常用命令
- 打印
```
#!/bin/bash
echo "Hello World !"
```
- 作为可执行程序
```
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```
- 作为解释器参数
```
/bin/sh test.sh
/bin/php test.php
```
- Shell变量
```

```
创建文件夹
```
mkdir [-p] dirName
参数说明：
p 确保目录名称存在，不存在的就建一个。
```

强制踢人

```
一、查看用户 
inux系统root用户可强制踢制其它登录用户，首先可用w命令查看登录用户信息
root@musicoder:/home/ju# w
二、强制踢人
命令格式：pkill -kill -t tty
解释：
pkill -kill -t 　踢人命令
tty　所踢用户的tty
比如： pkill -kill -t pts/2
```

查看系统版本

```
cat /proc/version
uname -a
lsb_release -a，即可列出所有版本信息
cat /etc/redhat-release，这种方法只适合Redhat系的Linux：
cat /etc/issue，此命令也适用于所有的Linux发行版。
```







# Linux crontab 命令
## 

```
crontab [ -u user ] { -l | -r | -e }
```
- e : 执行文字编辑器来设定时程表，内定的文字编辑器是 VI，如果你想用别的文字编辑器，则请先设定 VISUAL 环境变数来指定使用那个文字编辑器(比如说 setenv VISUAL joe)
- r : 删除目前的时程表
- l : 列出目前的时程表
- https://www.runoob.com/linux/linux-comm-crontab.html
```
crontab -e
编辑任务，按i，进入编辑模式。

每分钟执行一次
*/1 * * * * /data/mongodb/mongodb_backup_all.sh
每天执行一次
0 0 */0 * * /data/mongodb/mongodb_backup_incremental.sh
每30分钟执行一次
*/30 * * * * /data/mongodb/mongodb_backup_incremental.sh

/data/mongodb/mongodb_restore_all.sh
/data/mongodb/mongodb_restore_incremental.sh

/var/spool/mail/root
/var/spool/cron/root

```
```
supervisorctl start server-main
supervisorctl start server-test
supervisorctl start server-test-xw

supervisorctl stop server-main
supervisorctl stop server-test
supervisorctl stop server-test-xw
```

# 问题
## 解决“/bin/bash^M: bad interpreter: No such file or directory”
- 在执行shell脚本时提示这样的错误主要是由于shell脚本文件是dos格式，即每一行结尾以\r\n来标识，而unix格式的文件行尾则以\n来标识。查看脚本文件是dos格式还是unix格式的几种办法。
  1. cat -A filename  从显示结果可以判断，dos格式的文件行尾为^M$，unix格式的文件行尾为$。
  1. od -t x1 filename 如果看到输出内容中存在0d 0a的字符，那么文件是dos格式，如果只有0a，则是unix格式。
  1. vi filename打开文件，执行 : set ff，如果文件为dos格式在显示为fileformat=dos，如果是unxi则显示为fileformat=unix。

- 解决方法：
  1. 使用linux命令dos2unix filename，直接把文件转换为unix格式
  1. 使用sed命令sed -i "s/\r//" filename  或者 sed -i "s/^M//" filename直接替换结尾符为unix格式
  1. vi filename打开文件，执行 : set ff=unix 设置文件为unix，然后执行:wq，保存成unix格式。
