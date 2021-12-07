```sql
--在windows系统中写存储过程时，如果需要使用declare声明变量，需要添加这个关键字，否则会报错。
delimiter //
drop procedure if exists StatisticStore;
CREATE PROCEDURE StatisticStore()
BEGIN
	--创建接收游标数据的变量
	declare c int;
	declare n varchar(20);
	--创建总数变量
	declare total int default 0;
	--创建结束标志变量
	declare done int default false;
	--创建游标
	declare cur cursor for select name,count from store where name = 'iphone';
	--指定游标循环结束时的返回值
	declare continue HANDLER for not found set done = true;
	--设置初始值
	set total = 0;
	--打开游标
	open cur;
	--开始循环游标里的数据
	read_loop:loop
	--根据游标当前指向的一条数据
	fetch cur into n,c;
	--判断游标的循环是否结束
	if done then
		leave read_loop;	--跳出游标循环
	end if;
	--获取一条数据时，将count值进行累加操作，这里可以做任意你想做的操作，
	set total = total + c;
	--结束游标循环
	end loop;
	--关闭游标
	close cur;
 
	--输出结果
	select total;
END;
--调用存储过程
call StatisticStore();
```

![image-20211115142632016](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211115142632016.png)

![image-20211121151230315](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211121151230315.png)

