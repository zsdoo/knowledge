```sql
--MS Sql Server 查询数据库中所有表数据行数
--1
SELECT a.name,b.rows FROM sysobjects a  
INNER JOIN sysindexes b ON a.id=b.id   
WHERE b.indid IN(0,1) AND a.Type='u'  
ORDER BY b.rows desc

select * from sysobjects
--2
CREATE TABLE #temp (TableName VARCHAR (255), RowCnt INT)
EXEC sp_MSforeachtable 'INSERT INTO #temp SELECT ''?'', COUNT(*) FROM ?'

select * from #temp order by RowCnt desc
DROP TABLE #temp

--查询所有的表名及空间占用量情况
SELECT  OBJECT_NAME(id) tablename ,
        8 * reserved / 1024 reserved ,
        RTRIM(8 * dpages) AS 'used(kb)' ,
        8 * ( reserved - dpages ) / 1024 unused ,
        8 * dpages / 1024 - rows / 1024 * minlen / 1024 free
FROM    sysindexes
WHERE   indid = 1
ORDER BY reserved DESC 


--3、查看某个数据库，直接执行存储过程sp_spaceused即可

exec sp_spaceused;

--4、查看某个表，在存储过程后面加上表名即可

EXEC sp_spaceused 'student';
```







![image-20211009105508533](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009105508533.png)

![image-20211009105941930](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009105941930.png)

![image-20211009110204009](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009110204009.png)

![image-20211009110907792](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009110907792.png)

![image-20211009110942677](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009110942677.png)

C:\Program Files\Microsoft SQL Server\150\Setup Bootstrap\Log\20211009_110412\ConfigurationFile.ini

![image-20211009111402607](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211009111402607.png)



#### P1

![image-20211017224819006](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224819006.png)



![image-20211017224750009](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224750009.png)





![image-20211017224836470](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224836470.png)



![image-20211017224857594](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224857594.png)

![image-20211017225045844](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225045844.png)



![image-20211017225200361](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225200361.png)

##### 分离与附加

![image-20211017225321444](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225321444.png)



![image-20211017225352834](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225352834.png)



![image-20211017225414236](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225414236.png)

![image-20211017225441408](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225441408.png)

![image-20211017225458959](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017225458959.png)





#### P2-3 数据类型和完整性

![image-20211017221918686](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221918686.png)

![image-20211017222229688](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222229688.png)



![image-20211017222245803](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222245803.png)

![image-20211017222305423](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222305423.png)





![image-20211017222326625](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222326625.png)

![image-20211017222348210](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222348210.png)



![image-20211017222436223](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222436223.png)



![image-20211017222504678](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222504678.png)



![image-20211017222545819](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222545819.png)

#### p4  导出数据

![image-20211017222652405](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222652405.png)



![image-20211017222808893](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222808893.png)





![image-20211017222832186](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222832186.png)



![image-20211017222856570](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222856570.png)







<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017222916713.png" alt="image-20211017222916713" style="zoom:50%;" />



![image-20211017223511179](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017223511179.png)



























![image-20211010204536139](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010204536139.png)

![image-20211010204846640](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010204846640.png)

![image-20211010205303337](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010205303337.png)

![image-20211010205354852](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010205354852.png)

![image-20211010205442854](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010205442854.png)

![image-20211010210024527](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210024527.png)

![image-20211010210132523](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210132523.png)

![image-20211010210138659](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210138659.png)

![image-20211010210708701](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210708701.png)

![image-20211010210929431](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210929431.png)

![image-20211010210935386](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010210935386.png)

![image-20211010211050468](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010211050468.png)

![image-20211010211249293](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010211249293.png)

![image-20211010211335505](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010211335505.png)

![image-20211010211726143](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010211726143.png)



### 高级教程

#### p1

![image-20211010213953574](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010213953574.png)

![image-20211010214106208](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010214106208.png)

![image-20211010214209974](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010214209974.png)

![image-20211010214216334](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010214216334.png)

```sql
create database myschool002
on primary
(
	name='myschool_data',
	filename='D:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\myschool_data.mdf',
	size=5MB,
	maxsize=100MB,
	filegrowth=15%
)
log on
(
	name='myschool_log',
	filename='D:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\myschool_log.ldf',
	size=2MB,
	filegrowth=1MB
)
go
```



![image-20211010214645744](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010214645744.png)

![image-20211010214700714](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010214700714.png)

![image-20211010215104472](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211010215104472.png)



<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011213818644.png" alt="image-20211011213818644" style="zoom:67%;" />

![image-20211011213924957](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011213924957.png)

![image-20211011214004746](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011214004746.png)

```sql
use myschool002
go

--if exists (select * from sysobjects where name = 'student')
--	drop table student
--drop table if exists student

create table student
(
	studentno int not null,
	studentname varchar(50) not null,
	loginpwd varchar(50) not null,
	sex int not null, --性别： 0 -男 1-女 2 -保密 
	gradeid int not null,
	phone varchar(15),
	borndate datetime,
	address varchar(100),
	email varchar(50),
	identitycard char(18) not null
)
go
```

![image-20211011215009038](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011215009038.png)

![image-20211011223207638](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011223207638.png)

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011223244673.png" alt="image-20211011223244673" style="zoom: 67%;" />

![image-20211011223332060](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011223332060.png)

![image-20211011224157584](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011224157584.png)

![image-20211011224345171](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011224345171.png)

```sql
alter table student 
	add constraint pk_studentno primary key(studentno)

alter table grade 
	add constraint pk_gradeid primary key(gradeid)

alter table student 
	add constraint fk_gradid foreign key(gradeid) references grade(gradeid)
```



![image-20211011224350938](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011224350938.png)

![image-20211011225517549](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211011225517549.png)

#### p6三大范式

![image-20211017224320154](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224320154.png)



![image-20211017224402041](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224402041.png)

![image-20211017224418779](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224418779.png)



![image-20211017224440027](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224440027.png)

![image-20211017224506696](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017224506696.png)







#### p9  T sql

![image-20211014230634910](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014230634910.png)

![image-20211014230646171](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014230646171.png)

![image-20211014231058768](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231058768.png)

![image-20211014231134848](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231134848.png)



![image-20211014231428705](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231428705.png)

![image-20211014231550929](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231550929.png)

![image-20211014231758247](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231758247.png)

![image-20211014231835866](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014231835866.png)

![image-20211014232147579](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232147579.png)

![image-20211014232315502](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232315502.png)

![image-20211014232324410](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232324410.png)

![image-20211014232419311](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232419311.png)

![image-20211014232459367](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232459367.png)

![image-20211014232900649](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211014232900649.png)



#### p10 逻辑控制语句 

![image-20211017204938366](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017204938366.png)

![image-20211017204945991](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017204945991.png)

![image-20211017205103116](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205103116.png)

![image-20211017205736477](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205736477.png)

![image-20211017205700239](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205700239.png)

![image-20211017205746639](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205746639.png)

![image-20211017205813510](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205813510.png)

![image-20211017205818959](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017205818959.png)

![image-20211017210730215](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017210730215.png)

![image-20211017210741352](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017210741352.png)

![image-20211017210800347](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017210800347.png)

![image-20211017211616041](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017211616041.png)

![image-20211017211636488](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017211636488.png)

![image-20211017211826055](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017211826055.png)



#### p11-12 事务

![image-20211017211908449](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017211908449.png)

![image-20211017211925157](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017211925157.png)

![image-20211017212154601](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212154601.png)

![image-20211017212215394](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212215394.png)

![image-20211017212416492](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212416492.png)

![image-20211017212350676](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212350676.png)

![image-20211017212426376](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212426376.png)

![image-20211017212444552](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212444552.png)

![image-20211017212528543](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212528543.png)

![image-20211017212659305](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212659305.png)

![image-20211017212724797](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212724797.png)

![image-20211017212810036](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212810036.png)

![image-20211017212846315](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017212846315.png)

![image-20211017213005247](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213005247.png)

![image-20211017213302748](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213302748.png)

![image-20211017213417088](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213417088.png)

![image-20211017213515830](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213515830.png)

#### p13 视图

![image-20211017213625055](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213625055.png)

![image-20211017213701351](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213701351.png)

![image-20211017213730916](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213730916.png)

![image-20211017213750903](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213750903.png)

![image-20211017213904279](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017213904279.png)

![image-20211017214019132](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017214019132.png)

![image-20211017214131136](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017214131136.png)

![image-20211017214635488](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017214635488.png)

![image-20211017214658708](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017214658708.png)

#### p14 索引

![image-20211017215213927](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017215213927.png)



![image-20211017215237979](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017215237979.png)

![image-20211017215935345](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017215935345.png)

![image-20211017220927157](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017220927157.png)

![image-20211017221000170](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221000170.png)

![image-20211017221111250](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221111250.png)

![image-20211017221252723](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221252723.png)

![image-20211017221423129](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221423129.png)

![image-20211017221517477](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221517477.png)

![image-20211017221522562](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221522562.png)![image-20211017221559187](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221559187.png)

![image-20211017221644623](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221644623.png)

![image-20211017221658945](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211017221658945.png)

