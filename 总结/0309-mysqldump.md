```sql
 mysqldump -uroot -proot balance return_acc_c142 -w"CUST_ORDER_ACCOUNT_ID<223594244" --compact > return_acc_c142_bak0309_zsd.sql
 
 --从一个库中找个表，导入到另一个库中. where 条件中可以加limit
 mysqldump -uroot -proot balance return_acc_c142 -w"CUST_ORDER_ACCOUNT_ID<223594244" --compact | mysql -uroot -proot buss_interface;
 
 mysqldump -uroot -proot balance alipay_billing_detail -w"DATE_FORMAT(create_date,'%Y%m%d')='20201216' limit 50 " | mysql -uroot -proot buss_interface
 
 
 --0310
 mysqldump -uroot -proot balance --single-transaction --quick --compact --compress --extended-insert=false > backup_balance_0310_trans_compact_press_exte.sql
 
 
```

