卸载：https://blog.csdn.net/anzhen0429/article/details/76302158

安装：https://www.cnblogs.com/heyongboke/p/9946722.html



（3） rpm 安装

这种安装方法比较简单，只需下载相应的rpm安装包安装即可（注意根据提示安装相应的依赖包）。其中需要的 libev.so.4() 安装包：链接: https://pan.baidu.com/s/1PjO7CFwAa7Y1vvSUZk7weg 提取码: 47ja 

安装依赖：

```sql
wget ftp://rpmfind.net/linux/atrpms/el6-x86_64/atrpms/stable/libev-4.04-2.el6.x86_64.rpm
rpm -ivh libev-4.04-2.el6.x86_64.rpm

rpm -ivh libev-4.15-1.el6.rf.x86_64.rpm
yum install perl-DBI
yum -y install perl perl-devel libaio libaio-devel perl-Time-HiRes perl-DBD-MySQL
yum -y install perl-Digest-MD5

```



![image-20211206133850964](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211206133850964.png)

```bash
rpm -ivh percona-xtrabackup-24-2.4.10-1.el7.x86_64.rpm
```



## 完全备份

```bash
[root@linux-node1 backup]# xtrabackup --user=backup --password=123456 --databases=zabbix --backup --target-dir=/data/backup/xtrabackup/

xtrabackup  --user=root --password=root  --compress --backup --databases=test --target-dir=/home/backup/test >> /home/backup/backup.$(date +%F).log 2>&1
```

# xtrabackup命令用法实战https://blog.csdn.net/wfs1994/article/details/80399408



### 下面这个可以尝试，用新库测试

# 多实例部署与xtrabackup备份与恢复

https://www.jianshu.com/p/c856346a1477

