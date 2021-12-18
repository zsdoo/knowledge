## 一、[XtraBackup](https://www.dqzboy.com/tag/xtrabackup)介绍

https://www.dqzboy.com/1346.html

------

- Percona [XtraBackup](https://www.dqzboy.com/tag/xtrabackup)是一款基于MySQL的服务器的开源热备份实用程序，在备份过程中不会锁定数据库。它可以备份来自MySQL5.1，5.5，5.6和5.7服务器上的InnoDB，XtraDB和MyISAM表的数据，以及带有XtraDB的Percona服务器。

- Percona XtraBackup为所有版本的Percona Server，MySQL和MariaDB进行MySQL热备份。它执行流，压缩和增量MySQL备份。 

- 功能：
  - 在不暂停数据库的情况下创建热的InnoDB备份
  - 进行MySQL的增量备份
  - 将压缩的MySQL备份传输到另一台服务器
  - 在MySQL服务器之间移动表格
  - 轻松创建新的MySQL复制从站
  - 在不增加服务器负载的情况下备份MySQL

- Xtrabackup特点：
  - (1)备份过程快速、可靠
  - (2)备份过程不会打断正在执行的事务
  - (3)能够基于压缩等功能节约磁盘空间和流量
  - (4)自动实现备份检验
  - (5)还原速度快



### xtrabackup 选项

xtrabackup 工具有许多参数，具体可去官网查询（[xtrabackup 参数选项](https://www.percona.com/doc/percona-xtrabackup/LATEST/xtrabackup_bin/xbk_option_reference.html) | [innobackupex 参数选项](https://www.percona.com/doc/percona-xtrabackup/2.4/innobackupex/innobackupex_option_reference.html)），这里简单介绍 innobackupex 一些常用的参数。

**1) innobackupex 参数选项**

--defaults-file=[MY.CNF]   //指定配置文件：只能从给定的文件中读取默认选项。 且必须作为命令行上的第一个选项；必须是一个真实的文件，它不能是一个符号链接。

--databases=#   //指定备份的数据库和表，格式为：--databases="db1[.tb1] db2[.tb2]" 多个库之间以空格隔开，如果此选项不被指定，将会备份所有的数据库。

--include=REGEXP   //用正则表达式的方式指定要备份的数据库和表，格式为 --include=‘^mydb[.]mytb’ ，对每个库中的每个表逐一匹配，因此会创建所有的库，不过是空的目录。--include 传递给 xtrabackup --tables。

--tables-file=FILE   //此选项的参数需要是一个文件名，此文件中每行包含一个要备份的表的完整名称，格式为databasename.tablename。该选项传递给 xtrabackup --tables-file，与--tables选项不同，只有要备份的表的库才会被创建。

注意：部分备份（--include、--tables-file、--database）需要开启 innodb_file_per_table 。

--compact   //创建紧凑型备份，忽略所有辅助索引页，只备份data page；通过--apply-log中重建索引--rebuild-indexs。

--compress   //此选项指示xtrabackup压缩备份的InnoDB数据文件，会生成 *.qp 文件。

--decompress   //解压缩qp文件，为了解压缩，必须安装 qpress 工具。 Percona XtraBackup不会自动删除压缩文件，为了清理备份目录，用户应手动删除 * .qp文件：find /data/backup -name "*.qp" | xargs rm。

--no-timestamp   //指定了这个选项备份将会直接存储在 BACKUP-DIR 目录，不再创建时间戳文件夹。

--apply-log   //应用 BACKUP-DIR 中的 xtrabackup_logfile 事务日志文件。一般情况下，在备份完成后，数据尚且不能用于恢复操作，因为备份的数据中可能会包含尚未提交的事务或已经提交但尚未同步至数据文件中的事务。因此，此时数据文件仍处于不一致状态。“准备”的主要作用正是通过回滚未提交的事务及同步已经提交的事务至数据文件使得数据文件处于一致性状态。

--use-memory=#   //此选项接受一个字符参数（1M/1MB,1G/1GB，默认100M），仅与--apply-log一起使用，该选项指定prepare时用于崩溃恢复（crash-recovery）的内存。

--copy-back   //拷贝先前备份所有文件到它们的原始路径。但原路径下不能有任何文件或目录，除非指定 --force-non-empty-directories 选项。

--force-non-empty-directories   //恢复时指定此选项，可使 --copy-back 和 --move-back 复制文件到非空目录，即原data目录下可以有其他文件，但是不能有与恢复文件中同名的文件，否则恢复失败。

--rsync   //此选项可优化本地文件（非InnoDB）的传输。rsync工具一次性拷贝所有非InnoDB文件，而不是为每个文件单独创建cp，在备份恢复很多数据库和表时非常高效。此选项不能和 --stream 一起使用。

--incremental   //这个选项告诉 xtrabackup 创建一个增量备份，而不是完全备份。它传递到 xtrabackup 子进程。当指定这个选项，可以设置 --incremental-lsn 或 --incremental-basedir。如果这2个选项都没有被指定，--incremental-basedir 传递给 xtrabackup 默认值，默认值为：基础备份目录的第一个时间戳备份目录。

--incremental-basedir=DIRECTORY   //该选项接受一个字符串参数，该参数指定作为增量备份的基本数据集的完整备份目录。它与 --incremental 一起使用。

--incremental-dir=DIRECTORY   //该选项接受一个字符串参数，该参数指定了增量备份将与完整备份相结合的目录，以便进行新的完整备份。它与 --incremental 选项一起使用。

--redo-only   //在“准备基本完整备份” 和 “合并所有的增量备份(除了最后一个增备)”时使用此选项。它直接传递给xtrabackup的 xtrabackup --apply-log-only 选项，使xtrabackup跳过"undo"阶段，只做"redo"操作。如果后面还有增量备份应用到这个全备,这是必要的。有关详细信息,请参阅xtrabackup文档。

--parallel=NUMBER-OF-THREADS   //此选项接受一个整数参数，指定xtrabackup子进程应用于同时备份文件的线程数。请注意，此选项仅适用于文件级别，也就是说，如果您有多个.ibd文件，则它们将被并行复制； 如果您的表一起存储在一个表空间文件中，它将不起作用。

**2) xtrabackup 参数选项**

--apply-log-only   //这个选项使在准备备份(prepare)时，只执行重做(redo)阶段，这对于增量备份非常重要。



----





卸载：https://blog.csdn.net/anzhen0429/article/details/76302158

安装：https://www.cnblogs.com/heyongboke/p/9946722.html



#### （3） rpm 安装（最终用的此方式）

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



##### 完全备份（不对）

```bash
[root@linux-node1 backup]# xtrabackup --user=backup --password=123456 --databases=zabbix --backup --target-dir=/data/backup/xtrabackup/

xtrabackup  --user=root --password=root  --compress --backup --databases=test --target-dir=/home/backup/test >> /home/backup/backup.$(date +%F).log 2>&1
```

#### xtrabackup命令用法实战https://blog.csdn.net/wfs1994/article/details/80399408



### 下面这个可以尝试，用新库测试

##### 多实例部署与xtrabackup备份与恢复https://www.jianshu.com/p/c856346a1477

https://blog.csdn.net/huaying927/article/details/104215222?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_utm_term~default-4.no_search_link&spm=1001.2101.3001.4242.3



#### 进行全量备份

```bash
[root@node2 ~]# innobackupex --default-file=/etc/my.cnf --user=root --password=root --host=127.0.0.1 -P3306 /root/all
[root@node2 all]# pwd
/root/all

## 在恢复之前先检查事务日志
[root@node2 all]# innobackupex --apply-log /root/all/2021-12-09_15-50-16/

-- 备份腾讯云到本机的全备：
innobackupex --default-file=/etc/my.cnf --apply-log /home/work/2021-12-09_16-48-23/
innobackupex --default-file=/etc/my.cnf --copy-back -uroot -p -P3306 --host=127.0.0.1 --datadir=/opt/data/3306 /home/work/2021-12-09_16-48-23/

chown -R mysql.mysql /opt/data/3306
```



在执行恢复命令之前要先将/opt/data/3306/目录下的文件和目录清空

```bash
[root@node2 all]# cd /opt/data/3306/
[root@node2 3306]# rm -rf *
```



##### 恢复命令

```bash
[root@node2 all]# innobackupex --default-file=/etc/my.cnf --copy-back -uroot -p -P3306 --host=127.0.0.1 --datadir=/opt/data/3306 /root/all/2021-12-09_15-50-16/
```



发现3306目录下的文件和目录都恢复了，再到数据库去查看

```bash
更改目录属主和属组
[root@node2 3306]# chown -R mysql.mysql /opt/data/3306

[root@node2 all]# cd /opt/data/3306/
[root@node2 3306]# ls
ib_buffer_pool  ib_logfile1  performance_schema  xtrabackup_info
ibdata1         ibtmp1       sys                 xtrabackup_master_key_id
ib_logfile0     mysql        test

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+
5 rows in set (0.00 sec)
```



### 增量备份



```bash
# 先全备
[root@node2 3306]# innobackupex --user=root --password=root --host=127.0.0.1 /root/all/
##	2021-12-09_16-16-44

# 使用innobackup进行增量备份
[root@node2 3306]# innobackupex --user=root --password=root --default-file=/etc/my.cnf --host=127.0.0.1 --incremental /root/all/ --incremental-basedir=/root/all/2021-12-09_16-16-44/
--incremental /root/all/ -- 备份位置
--incremental-basedir=/root/all/2021- -- 全备名称


[root@k8s-master 2021-12-09_16-16-44]# cat xtrabackup_checkpoints 
backup_type = full-backuped  #备份类型为全量备份
from_lsn = 0  #lsn从0开始
to_lsn = 2757173  #lsn到2757182结束
last_lsn = 2757182
compact = 0
recover_binlog_info = 0

#增量备份的xtrabackup_checkpoints 
[root@k8s-master all]# cd 2021-12-09_16-26-36/
[root@k8s-master 2021-12-09_16-26-36]# cat xtrabackup_checkpoints 
backup_type = incremental  #备份类型为增量备份
from_lsn = 2757173  #lsn从2757173开始
to_lsn = 2759882  lsn到2759882结束
last_lsn = 2759891
compact = 0
recover_binlog_info = 0
[root@k8s-master 2021-12-09_16-26-36]# 
```

模拟数据库故障，关闭数据库

```csharp
[root@node2 3306]# pkill mysqld
删除数据目录中的所有数据
[root@node2 3306]# pwd
/opt/data/3306
[root@node2 3306]# rm -rf *
```



##### 合并全备数据目录，确保数据的一致性

```bash
[root@node2 3306]# innobackupex --apply-log --redo-only /root/all/2021-12-09_16-16-44/
```

##### 将增量备份的数据合并到全备数据目录当中

```bash
[root@node2 3306]# innobackupex --apply-log --redo-only /root/all/2021-12-09_16-16-44/ --incremental-dir=/root/all/2021-12-09_16-26-36/

[root@k8s-master 2021-12-09_16-16-44]# cat xtrabackup_checkpoints 
backup_type = log-applied  #查看到数据备份类型是增加
from_lsn = 0  #lsn从0开始
to_lsn = 2759882  #lsn结束号为最新的lsn
last_lsn = 2759891
compact = 0
recover_binlog_info = 0
[root@k8s-master 2021-12-09_16-16-44]# 
```



##### 恢复数据

```ruby
[root@node2 3306]# 
innobackupex --default-file=/etc/my.cnf --copy-back -uroot -p -P3306 --host=127.0.0.1 --datadir=/opt/data/3306 /root/all/2021-12-09_16-16-44/

innobackupex --default-file=/etc/my.cnf --copy-back -uroot -proot -h127.0.0.1 -P3306 --datadir=/opt/data/3306 /root/all/2021-12-09_16-16-44/

更改目录属主和属组
[root@node2 3306]# chown -R mysql.mysql /opt/data/3306
启动MySQL
[root@node2 support-files]# ./mysql.server start
[root@node2 support-files]# pwd
/usr/src/mysql/support-files
查看数据的恢复
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+
5 rows in set (0.00 sec)

mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| xx             |
+----------------+
1 row in set (0.00 sec)
```



作者：12138
链接：https://www.jianshu.com/p/c856346a1477
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

##### 更改目录属主和属组： chown -R mysql.mysql /opt/data/3306

### 测试全备及多次增量备份1210

```sql
#1 全备: innobackupex --host=127.0.0.1 -uroot -proot /root/all
#  2021-12-10_11-27-18

#2 一次增量： innobackupex --default-file=/etc/my.cnf --host=127.0.0.1 --user=root --password=root --incremental /root/all/ --incremental-basedir=/root/all/2021-12-10_11-27-18
#3 二次增量：innobackupex --default-file=/etc/my.cnf --host=127.0.0.1 --user=root --password=root --incremental /root/all/ --incremental-basedir=/root/all/2021-12-10_11-45-21
#4 三次增量：innobackupex --default-file=/etc/my.cnf --host=127.0.0.1 --user=root --password=root --incremental /root/all/ --incremental-basedir=/root/all/2021-12-10_11-46-46
## 2021-12-10_13-36-52

合并备份数据目录
# 合并备份数据目录(可陆续将增量文件合并到全备中)（但增量文件不能合并入增量文件！！！）
 innobackupex --apply-log --redo-only /root/all/2021-12-10_11-27-18/ --incremental-dir=/root/all/2021-12-10_11-45-21/
 
 innobackupex --apply-log --redo-only /root/all/{第一次的全备文件}/ --incremental-dir=/root/all/{第二次的备份文件}
 innobackupex --apply-log --redo-only /root/all/{第一次的全备文件}/ --incremental-dir=/root/all/{第三次的备份文件}
  恢复：
innobackupex  --copy-back  --datadir=/opt/data/3306 /root/all/2021-12-10_11-27-18

更改目录属主和属组： chown -R mysql.mysql /opt/data/3306

--1 指定两个库：
innobackupex --host=127.0.0.1 -uroot -proot --databases="test temps" /root/all
--2 第一次增量：
innobackupex --default-file=/etc/my.cnf --host=127.0.0.1 --user=root --password=root --databases="test temps" --incremental /root/all/ --incremental-basedir=/root/all/2021-12-10_15-56-34
--3 第一次增量：
innobackupex --default-file=/etc/my.cnf --host=127.0.0.1 --user=root --password=root --databases="test temps" --incremental /root/all/ --incremental-basedir=/root/all/2021-12-10_16-00-59

--4 合并备份数据目录
# 合并备份数据目录(可陆续将增量文件合并到全备中)（但增量文件不能合并入增量文件！！！）
--4.1 innobackupex --apply-log --redo-only /root/all/2021-12-10_15-56-34/
--4.2 innobackupex --apply-log --redo-only /root/all/2021-12-10_15-56-34/ --incremental-dir=/root/all/2021-12-10_16-00-59/
--4.3 innobackupex --apply-log --redo-only /root/all/2021-12-10_15-56-34/ --incremental-dir=/root/all/2021-12-10_16-05-28/


```



#### 单表备份：

##### 利用XtraBackup做全量备份、增量备份、数据目录相同恢复、数据目录不同恢复、单表备份恢复

https://blog.csdn.net/wukong_666/article/details/71557038



mkdir -p /home/backup/table_only
innobackupex --defaults-file=/usr/local/mysql/my.cnf --include='sbtest.test' --user=root --password=123 /home/backup/table_only/

```sql
mkdir -p /root/all/only

#备份单表
innobackupex --defaults-file=/etc/my.cnf  --include='test.form' --host=127.0.0.1 --user=root --password=root  /root/all/only
```



[root@host-192-168-1-21 2017-05-10_05-13-27]# ls /home/backup/table_only/2017-05-10_05-13-27/  #只备份了sbtest的test表
backup-my.cnf  ib_buffer_pool  IBdata1  IBdata2  sbtest  xtrabackup_binlog_info  xtrabackup_checkpoints  xtrabackup_info  xtrabackup_logfile
[root@host-192-168-1-21 2017-05-10_05-13-27]# cat xtrabackup_info 其中有一行 partial = Y 
apply-log之前：[root@host-192-168-1-21 2017-05-10_05-13-27]# cat xtrabackup_checkpoints 第一行为backup_type = full-backuped
apply-log之后变为backup_type = full-prepared
innobackupex --apply-log --export /home/backup/table_only/2017-05-10_05-13-27/

```sql
#应用日志
innobackupex --apply-log /root/all/only/2021-12-10_15-02-11
```

[root@host-192-168-1-21 sbtest]# ls /home/backup/table_only/2017-05-10_05-13-27/sbtest/
test.cfg  test.exp  test.frm  test.ibd
mysql> select * from test;

3 rows in set (0.00 sec)
mysql>  delete from test where id in (2,3);
Query OK, 2 rows affected (0.02 sec)
mysql> select * from test;
1 row in set (0.00 sec)
mysql> alter table test discard tablespace;
Query OK, 0 rows affected (0.03 sec)

```sql
# 删除表空间
alter table form DISCARD TABLESPACE;
SELECT * from form;
> Tablespace has been discarded for table 'form'
# 复制表空间
 cp form.ibd /opt/data/3306/test/
 
# 导入表空间后，查询成功
alter table form import TABLESPACE;
```

mysql> select * from test;
ERROR 1814 (HY000): Tablespace has been discarded for table 'test'
cp /home/backup/table_only/2017-05-10_05-13-27/sbtest/test.{cfg,ibd} /data/mysql/data_test/sbtest/
chown mysql:mysql /data/mysql/data_test/sbtest/test.*
mysql> alter table test import tablespace;
Query OK, 0 rows affected (0.15 sec)

----

http://t.zoukankan.com/longshiyVip-p-5128777.htmlPercona Xtrabackup备份mysql全库及指定数据库(完整备份与增量备份)





#### 备份脚本：

```bash
#!/bin/sh
# add ling
# xtraback 全备
INNOBACKUPEX=innobackupex
INNOBACKUPEXFULL=/usr/bin/$INNOBACKUPEX
TODAY=`date +%Y%m%d%H%M`
YESTERDAY=`date -d"yesterday" +%Y%m%d%H%M`
USEROPTIONS="--user=user --password=123456"
TMPFILE="/logs/mysql/innobackup_$TODAY.$$.tmp"
MYCNF=/etc/my.cnf
MYSQL=/usr/local/mariadb/bin/mysql
MYSQLADMIN=/usr/local/mariadb/bin/mysqladmin
BACKUPDIR=/backup/mysql # 备份的主目录
FULLBACKUPDIR=$BACKUPDIR/full # 全库备份的目录
INCRBACKUPDIR=$BACKUPDIR/incr # 增量备份的目录
KEEP=1 # 保留几个全库备份
 
# Grab start time
#############################################################################
# Display error message and exit
#############################################################################
error()
{
    echo "$1" 1>&2
    exit 1
}
 
# Check options before proceeding
if [ ! -x $INNOBACKUPEXFULL ]; then
  error "$INNOBACKUPEXFULL does not exist."
fi
 
if [ ! -d $BACKUPDIR ]; then
  error "Backup destination folder: $BACKUPDIR does not exist."
fi
 
if [ -z "`$MYSQLADMIN $USEROPTIONS status | grep 'Uptime'`" ] ; then
 error "HALTED: MySQL does not appear to be running."
fi
 
if ! `echo 'exit' | $MYSQL -s $USEROPTIONS` ; then
 error "HALTED: Supplied mysql username or password appears to be incorrect (not copied here for security, see script)."
fi
 
# Some info output
echo "----------------------------"
echo
echo "$0: MySQL backup script"
echo "started: `date`"
echo
 
# Create full and incr backup directories if they not exist.
for i in $FULLBACKUPDIR $INCRBACKUPDIR
do
        if [ ! -d $i ]; then
                mkdir -pv $i
        fi
done
 
# 压缩上传前一天的备份
echo "压缩前一天的备份，scp到远程主机"
cd $BACKUPDIR
tar -zcvf $YESTERDAY.tar.gz ./full/ ./incr/
scp -P 8022 $YESTERDAY.tar.gz root@192.168.10.46:/data/backup/mysql/
if [ $? = 0 ]; then
  rm -rf $BACKUPDIR/full $BACKUPDIR/incr
  echo "Running new full backup."
  innobackupex --defaults-file=$MYCNF $USEROPTIONS $FULLBACKUPDIR > $TMPFILE 2>&1
else
  echo "Error with scp."
fi
 
if [ -z "`tail -1 $TMPFILE | grep 'completed OK!'`" ] ; then
 echo "$INNOBACKUPEX failed:"; echo
 echo "---------- ERROR OUTPUT from $INNOBACKUPEX ----------"
# cat $TMPFILE
# rm -f $TMPFILE
 exit 1
fi
 
# 这里获取这次备份的目录 
THISBACKUP=`awk -- "/Backup created in directory/ { split( \\\$0, p, \"'\" ) ; print p[2] }" $TMPFILE`
echo "THISBACKUP=$THISBACKUP"
#rm -f $TMPFILE
echo "Databases backed up successfully to: $THISBACKUP"
 
# Cleanup
echo "delete tar files of 3 days ago"
find $BACKUPDIR/ -mtime +3 -name "*.tar.gz"  -exec rm -rf {} \;
 
echo
echo "completed: `date`"
exit 0



================
# xtraback 全备

#!/bin/sh
# add ling
 
INNOBACKUPEX=innobackupex
INNOBACKUPEXFULL=/usr/bin/$INNOBACKUPEX
TODAY=`date +%Y%m%d%H%M`
USEROPTIONS="--user=user --password=123456"
TMPFILE="/logs/mysql/incr_$TODAY.$$.tmp"
MYCNF=/etc/my.cnf
MYSQL=/usr/local/mariadb/bin/mysql
MYSQLADMIN=/usr/local/mariadb/bin/mysqladmin
BACKUPDIR=/backup/mysql # 备份的主目录
FULLBACKUPDIR=$BACKUPDIR/full # 全库备份的目录
INCRBACKUPDIR=$BACKUPDIR/incr # 增量备份的目录
 
#############################################################################
# Display error message and exit
#############################################################################
error()
{
    echo "$1" 1>&2
    exit 1
}
 
# Check options before proceeding
if [ ! -x $INNOBACKUPEXFULL ]; then
  error "$INNOBACKUPEXFULL does not exist."
fi
 
if [ ! -d $BACKUPDIR ]; then
  error "Backup destination folder: $BACKUPDIR does not exist."
fi
 
if [ -z "`$MYSQLADMIN $USEROPTIONS status | grep 'Uptime'`" ] ; then
 error "HALTED: MySQL does not appear to be running."
fi
 
if ! `echo 'exit' | $MYSQL -s $USEROPTIONS` ; then
 error "HALTED: Supplied mysql username or password appears to be incorrect (not copied here for security, see script)."
fi
 
# Some info output
echo "----------------------------"
echo
echo "$0: MySQL backup script"
echo "started: `date`"
echo
 
# Create full and incr backup directories if they not exist.
for i in $FULLBACKUPDIR $INCRBACKUPDIR
do
        if [ ! -d $i ]; then
                mkdir -pv $i
        fi
done
 
# Find latest full backup
LATEST_FULL=`find $FULLBACKUPDIR -mindepth 1 -maxdepth 1 -type d -printf "%P\n"`
echo "LATEST_FULL=$LATEST_FULL" 
 
# Run an incremental backup if latest full is still valid.
# Create incremental backups dir if not exists.
TMPINCRDIR=$INCRBACKUPDIR/$LATEST_FULL
mkdir -p $TMPINCRDIR
BACKTYPE="incr"
# Find latest incremental backup.
LATEST_INCR=`find $TMPINCRDIR -mindepth 1 -maxdepth 1 -type d | sort -nr | head -1`
echo "LATEST_INCR=$LATEST_INCR"
  # If this is the first incremental, use the full as base. Otherwise, use the latest incremental as base.
if [ ! $LATEST_INCR ] ; then
  INCRBASEDIR=$FULLBACKUPDIR/$LATEST_FULL
else
  INCRBASEDIR=$LATEST_INCR
fi
echo "Running new incremental backup using $INCRBASEDIR as base."
innobackupex --defaults-file=$MYCNF $USEROPTIONS --incremental $TMPINCRDIR --incremental-basedir $INCRBASEDIR > $TMPFILE 2>&1
 
 
if [ -z "`tail -1 $TMPFILE | grep 'completed OK!'`" ] ; then
 echo "$INNOBACKUPEX failed:"; echo
 echo "---------- ERROR OUTPUT from $INNOBACKUPEX ----------"
 exit 1
fi
 
# 这里获取这次备份的目录 
THISBACKUP=`awk -- "/Backup created in directory/ { split( \\\$0, p, \"'\" ) ; print p[2] }" $TMPFILE`
echo "THISBACKUP=$THISBACKUP"
echo
echo "Databases backed up successfully to: $THISBACKUP"
 
echo
echo "incremental completed: `date`"
exit 0
```





