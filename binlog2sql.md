https://gitee.com/liangguifeng/binlog2sql?_from=gitee_search



### 选项

**mysql连接配置**

-h host; -P port; -u user; -p password

**解析模式**

--stop-never 持续解析binlog。可选。默认False，同步至执行命令时最新的binlog位置。

-K, --no-primary-key 对INSERT语句去除主键。可选。默认False

-B, --flashback 生成回滚SQL，可解析大文件，不受内存限制。可选。默认False。与stop-never或no-primary-key不能同时添加。

--back-interval -B模式下，每打印一千行回滚SQL，加一句SLEEP多少秒，如不想加SLEEP，请设为0。可选。默认1.0。

**解析范围控制**

--start-file 起始解析文件，只需文件名，无需全路径 。必须。

--start-position/--start-pos 起始解析位置。可选。默认为start-file的起始位置。

--stop-file/--end-file 终止解析文件。可选。默认为start-file同一个文件。若解析模式为stop-never，此选项失效。

--stop-position/--end-pos 终止解析位置。可选。默认为stop-file的最末位置；若解析模式为stop-never，此选项失效。

--start-datetime 起始解析时间，格式'%Y-%m-%d %H:%M:%S'。可选。默认不过滤。

--stop-datetime 终止解析时间，格式'%Y-%m-%d %H:%M:%S'。可选。默认不过滤。

**对象过滤**

-d, --databases 只解析目标db的sql，多个库用空格隔开，如-d db1 db2。可选。默认为空。

-t, --tables 只解析目标table的sql，多张表用空格隔开，如-t tbl1 tbl2。可选。默认为空。

--only-dml 只解析dml，忽略ddl。可选。默认False。

--sql-type 只解析指定类型，支持INSERT, UPDATE, DELETE。多个类型用空格隔开，如--sql-type INSERT DELETE。可选。默认为增删改都解析。用了此参数但没填任何类型，则三者都不解析。

### 应用案例

#### **误删整张表数据，需要紧急回滚**

闪回详细介绍可参见example目录下《闪回原理与实战》[example/mysql-flashback-priciple-and-practice.md](https://gitee.com/liangguifeng/binlog2sql/blob/master/example/mysql-flashback-priciple-and-practice.md)

```sql
insert into mylogbin2 (m_name,is_deleted) VALUES ('测试1',0);
insert into mylogbin2 (m_name,is_deleted) VALUES ('测试2',0);
insert into mylogbin2 (m_name,is_deleted) VALUES ('测试3',0);
insert into mylogbin2 (m_name,is_deleted) VALUES ('测试4',0);
SELECT * from mylogbin3
create table testabcd SELECT * from mylogbin3;
insert into mylogbin3 (m_name,is_deleted) VALUES ('测试15',0);
insert into mylogbin3 (m_name,is_deleted) VALUES ('测试16',0);
insert into mylogbin3 (m_name,is_deleted) VALUES ('测试17',0);
insert into mylogbin3 (m_name,is_deleted) VALUES ('测试18',0);

1 误删数据解析回复
-- 按时间、指定表查出数据
python binlog2sql.py -h127.0.0.1 -P3306 -uroot -p'root' -dtest --tables mylogbin2 --start-datetime='2021-12-01 14:30:00' --stop-datetime='2021-12-01 16:19:00' --start-file='mysql-bin.000005' | less
-- 解析出回滚SQL
python binlog2sql.py --flashback -h127.0.0.1 -P3306 -uroot -p'root' -dtest -t mylogbin2 --start-file='mysql-bin.000005' --start-datetime='2021-12-01 14:30:00' --stop-datetime='2021-12-01 16:19:00'

2 整表delete删除
SELECT * from mylogbin3;
delete from   mylogbin2; -- 16:32
insert into mylogbin3 (m_name,is_deleted) VALUES ('测试1111111111111111111111121',0);
# 查看：python binlog2sql.py -h127.0.0.1 -P3306 -uroot -p'root' -dtest --tables mylogbin2 --start-file='mysql-bin.000006' --start-datetime='2021-12-01 16:30:00' | less
show master status;
flush logs
python binlog2sql.py -h127.0.0.1 -P3306 -uroot -p'root' -dtest --tables mylogbin2 --start-file='mysql-bin.000006' --start-datetime='2021-12-01 16:30:00' -B > rollback.sql | cat

3 整表drop删除,无法使用binlog2sql !!! -- 只能使用mysqlbinlog
#SELECT * from mylogbin2;
#drop table mylogbin2;  -- 16:40 - 41

# mysqlbinlog -vv /usr/local/mysql/data/mysql-bin.000006 -d test --start-datetime="2021-12-01  16:40:00" --stop-datetime="2021-12-01  16:45:00" > mylog2.sql
python binlog2sql.py -h127.0.0.1 -P3306 -uroot -p'root' -dtest --tables mylogbin2 --start-datetime='2021-12-01 16:40:00' --stop-datetime='2021-12-01 16:43:00' --start-file='mysql-bin.000006' -B | less
#show master status;
#SELECT * from testabcd;
#update testabcd set is_deleted='1';

-- 用binlog恢复，可指定数据库，-f忽略错误执行
mysqlbinlog -vv  mysql-bin.000008 -d test --stop-position='2066' | mysql -uroot -proot -Dtest -f
```

#### 在从库授权后执行binlog --报错 -- 忽略仍报错

```sql
grant all privileges on test.testabcd to 'userabcd'@'localhost' identified by 'userabcd' with grant option;
select * from mysql.`user`
show grants for 'userabcd'@'%';

mysqlbinlog -vv  mysql-bin.000008 -d test --stop-position='2066' | mysql -h127.0.0.1 -uuserabcd -puserabcd -Dtest -f
```

