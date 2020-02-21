# Java运维
### 1. 【推荐】高并发服务器建议调小TCP协议的`time_wait`超时时间。
变更/etc/sysctl.conf文件去修改该缺省值（秒）：
```
net.ipv4.tcp_fin_timeout = 30
```
### 2. 【推荐】调大服务器所支持的最大文件句柄数
变更/etc/security/limits.conf文件  
添加如下内容：
```
* soft nofile 65536
* hard nofile 65536
```
然后重启  
```shell
sudo init 6
```

### 3. 【推荐】JVM推荐添加参数-Djava.security.egd=file:/dev/./urandom -XX:+HeapDumpOnOutOfMemoryError
-Djava.security.egd=file:/dev/./urandom：解决Linux随机数问题
-XX:+HeapDumpOnOutOfMemoryError：用于排查OOM

### 4. 【推荐】在线上生产环境，JVM的Xms和Xmx设置一样大小的内存容量
避免在GC后调整堆大小带来的压力。  

### 5. 【强制】日志文件至少保存15天
已备有些异常具备以“周”为频次发生的特点。