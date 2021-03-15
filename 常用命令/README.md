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

## 时区设置

查看系统时间

```
date
```

时区改成UTC

```
ln -sf /usr/share/zoneinfo/UTC /etc/localtime
```

中国时区CST，上海时区

```
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

## 文件夹改名

### 文件夹名folderA改为folderB

```
mv folderA folderB
```

## 查看文件任意几行数据

### 查看最后10行数据

```
cat filename | tail -n 10
```

### 查看10行到100行的数据

```
cat filename|head -n 10 | tail -n 100
```

### 最后10行

```
tail -n 10
```

### 文件第10行开始以后的内容

```
tail -n +10
```

### 前10行的内容

```
head -n 100
```





























