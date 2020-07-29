# 学习网址

- https://www.cnblogs.com/maifengqiang/p/3863168.html
- https://www.cnblogs.com/bakari/p/10748721.html
- https://www.cnblogs.com/ggjucheng/archive/2012/01/14/2322659.html

# 笔记
```
1.抓5432端口的包，不管是对方还是本机的5432端口。
tcpdump tcp port 5432
2.将抓的包保存到文件中
tcpdump tcp port 5432 -w ./postgres.cap
3.并让这个进程在后台运行
tcpdump tcp port 5432 -w ./postgres.cap &
```

```
1、可使用帮助文档里的示例
tcpdump -l >data & tail -f data
2、对ip过滤（目标ip：192.168.2.3），保存到文件里并即时输出
tcpdump -l host 192.168.2.3 >data &tail -f data
3、对ip及多网卡时网卡过滤（目标ip：192.168.2.3，网卡：eth3），保存到文件里并即时输出
tcpdump -l -i eth3 host 192.168.2.3 >data & tail -f data
4、后台运行，此时不能用tail查看，注意最后的"&"不要漏了
nohup tcpdump -l -i eth3 host 192.168.2.3 >data &
5、后台运行时结束进程
第一步：运行命令   ps -ef|grep tcpdump |grep -v 'grep'   可得到一个或多个进程，进程号为第二个参数（数字），第三个参数是它的父进程号
第二步：把第一步得到的进程逐个结束掉，命令为 kill -9  进程号
```

# 实例
```
tcpdump tcp -i eth0 port 5555 and src 113.65.228.241 -w ./target.cap
后台执行
nohup tcpdump -w ./target.cap &
nohup tcpdump tcp -i eth0 port 5555 and src 113.65.228.241 -w ./target.cap &
tcpdump tcp -i eth0 port 5555 and src 113.65.228.241 -w ./target.cap > ./t.cap &


tcpdump tcp -i eth0 port 5555 -w ./xql_regu.cap &
tcpdump tcp -i enp0s31f6 port 5573 -w ./xql_test.cap &

ps -aux|grep tcpdump
kill -9 进程id



```

