#### into outfile    

查看路径：show variables like 'datadir';



mysql -uroot -proot balance -e "select * from wx_funds_detail t WHERE t.account_date>= '2021-09-01 00:00:00' and business_type in ('企业代付','企业代付到银行卡退款') into outfile '/opt/mysql-5.7.26/data/1014_qidaifu.csv';"



#### mysqldump：

--extended-insert=FALSE  每行一个插入语句

--skip-comments 取消注释

--compact导出更少的输出信息

-t 不要写表格创建信息, 只生成插入数据的语句

--complete-insert,  -c
使用完整的insert语句(包含列名称)。



--set-gtid-purge=off 忽略GTID导出信息

mysqldump --single-transaction --set-gtid-purged=off --compact --complete-insert --extended-insert=FALSE -t -uroot -p'root' --databases balance --tables wx_funds_detail --where='date_format(account_date,'%Y%m')= "202109"' --where="business_type like '企业代付%'" >/root/data02/1014_wx_funds.sql



--set-gtid-purged=OFF