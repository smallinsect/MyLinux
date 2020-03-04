# MyLinux



# 查看进程详细信息
查看包含“server”的进程  
ps -aux | grep server  
查看包含“server”的id进程  
ps -ef | grep server

# 查看进程占用端口
netstat -nap | grep 20696  
