#### 启动

![image-20211120161458418](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120161458418.png)

![image-20211120162053801](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120162053801.png)

#### 信息头设置



![image-20211120202344201](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120202344201.png)

![image-20211120202304591](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120202304591.png)



<img src="D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120194519916.png" alt="image-20211120194519916" style="zoom: 67%;" />





#### 定义变量

![image-20211120201639067](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120201639067.png)

![image-20211120201819413](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120201819413.png)

![image-20211120201919515](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120201919515.png)

#### CSV

![image-20211120202114061](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120202114061.png)

![image-20211120203141741](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120203141741.png)

![image-20211120203230871](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120203230871.png)

![image-20211120203207683](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120203207683.png)



#### 用户参数

![image-20211120204036763](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120204036763.png)

![image-20211120204716853](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120204716853.png)



#### 函数

![image-20211120204737692](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120204737692.png)

![image-20211120205806071](D:\工作文件\knowledge\总结\Knowledge_pictrue\image-20211120205806071.png)



##### 时间函数：

${__time(,)}：获取当前时间的毫秒数；
${__time(,time_ms)}：获取当前时间的毫秒数并存入参数time_ms中；
${__time(/1000,)}：获取当前时间的秒数；
${__time(/1000,time_s)}：获取当前时间的秒数并存入参数time_s中；
${__time(yyyy-MM-dd,)}：获取当前日期；
${__time(yyyy-MM-dd,time_date1)}：获取当前日期并存入参数time_date1中；
${__time(yyyy-MM-dd HH:mm:ss,)}：获取当前时间，固定格式；
${__time(yyyyMMddHHmmss,time_2)}：获取当前时间，固定格式，并存入参数time_2中；
${__time(YMDHMS,)}：获取当前时间，固定格式




#### 直连数据库

##### 0引用jar包

使用JDBC Request时需要连接数据库的jar包，可以在Mysql的官网下载https://dev.mysql.com/downloads/file/?id=476198

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742061481620.png)





下面介绍一下Jmeter向mysql数据库中插入数据的入门操作。

1、新建一个线程组，这是必经步骤：

在测试计划上右键-->添加-->Theaders(Users)-->线程组

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70.png)

2、添加配置元件JDBC Connection Configuration

在线程组上右键-->添加-->配置元件-->JDBC Connection Configuration

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-16374204591952.png)

3、添加随机数生成元件：

在线程组上右键-->添加-->配置元件-->Random Variable

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-16374204660334.png)

4、添加JDBC Sampler：

在线程组上右键-->添加-->Sampler-->JDBC Request

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-16374204730606.png)

5、再添加一个监听器，添加完毕后，结构如下：

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-16374204780498.png)



上面是使用Jmeter向数据库中添加数据时需要的主要元件，接下来做一下各个元件的配置

##### 1、我们需要插入的数据量可以在线程组的线程数、循环次数进行配置，如下，这里只插入10条数据，使用循环10次进行控制

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742049926910.png)

##### 2、配置JDBC Connection Configuration

注意点：1、Variable Name 必填，否则后面无法请求；

2、JDBC url一定是正确的：jdbc:mysql://服务器地址:端口号/数据库名

3、选择数据库驱动，以mysql为例，其他数据库可以百度到对应的驱动

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742051086412.png)

3、设置随机变量：

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742058025914.png)

##### 4、配置JDBC Request:

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742058540316.png)

5、接下来就可以执行脚本了，可以查看在监听器中查看执行结果

![img](D:\工作文件\knowledge\总结\Knowledge_pictrue\70-163742059280218.png)





