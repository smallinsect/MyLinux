# MyLinux

## 命令笔记

查看包含“server”的进程
```
ps -aux | grep server
```

查看包含“server”的id进程

```
ps -ef | grep server
```

查看进程占用端口

```
netstat -nap|grep 20696
netstat -nap|grep mongod
```
创建文件夹

```
mkdir 文件名
```

杀掉进程

```
kill -9 pid
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
