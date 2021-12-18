### **linux 下查找大于100M的文件**

find . -type f -size +100M 查找当前目录下大于100M的文件,-type f表示文件类型

**显示当前目录或者文件夹的所占磁盘空间**：du -sh *

**显示前**10个占用空间最大的文件或目录: du -sh * | sort -nr | head

**查看内存**：top   | free -h  |   cat /proc/meminfo

**Linux查看当前操作系统版本信息** cat /proc/version

**Linux查看版本当前操作系统内核信息** **uname -a**

**linux查看版本当前操作系统发行信息** **cat /etc/issue 或 cat /etc/centos-release**

##### 防火墙和selinux

```sql
--查看防火墙状态命令：systemctl status firewalld.service
--关闭运行的防火墙: systemctl stop firewalld.service    
--开机禁止防火墙服务器: systemctl disable firewalld.service，
--开机启动防火墙服务器: systemctl enable firewalld.service，

查看selinux状态和临时关闭selinux
--getenforce 获取当前selinux状态 Enforcing为开启
--临时关闭运行命令 sudo setenforce 0

永久关闭selinux成功
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```



### **Linux查看cpu相关信息**

**包括型号、主频、内核信息等 cat /etc/cpuinfo**

### **scp:**

```bash
scp [可选参数] file_source file_target
-p：保留原文件的修改时间，访问时间和访问权限。
-r： 递归复制整个目录。
-v：详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。

scp -prv * ht@10.46.5.20:/data/toweralipay/data
scp -P 50022 -prv ht@10.46.5.20:/root/bak.tar.zip /data/
```

### **grep:**

```bash
--color=auto 或者 --color：表示对匹配到的文本着色显示
-i：在搜索的时候忽略大小写
-n：显示结果所在行号
-c：统计匹配到的行数，注意，是匹配到的总行数，不是匹配到的次数
-o：只显示符合条件的字符串，但是不整行显示，每个符合条件的字符串单独显示一行
-v：输出不带关键字的行（反向查询，反向匹配）
-w：匹配整个单词，如果是字符串中包含这个单词，则不作匹配
-Ax：在输出的时候包含结果所在行之后的指定行数，这里指之后的x行，A：after
-Bx：在输出的时候包含结果所在行之前的指定行数，这里指之前的x行，B：before
-Cx：在输出的时候包含结果所在行之前和之后的指定行数，这里指之前和之后的x行，C：context
-e：实现多个选项的匹配，逻辑or关系
-q：静默模式，不输出任何信息，当我们只关心有没有匹配到，却不关心匹配到什么内容时，我们可以使用此命令，然后，使用"echo $?"查看是否匹配到，0表示匹配到，1表示没有匹配到。
-P：表示使用兼容perl的正则引擎。
-E：使用扩展正则表达式，而不是基本正则表达式，在使用"-E"选项时，相当于使用egrep。
```

### sed

```bash
### 查两行之间：
sed -n '/11/,/44/p' file.txt
sed -n '/DROP TABLE IF EXISTS `alipay_account_detail`;/,/UNLOCK TABLES;/p'  /data/bak>/data/alipay_account_detail
使用正则表达式。
sed -n ‘/2010-11-17 09:[0-9][0-9]:[0-9][0-9]/,/2010-11-17 16:[0-9][0-9]:[0-9][0-9]/p’  logfile

{# mysql 导出与导入
整库备份导出：mysqldump -uroot -p --databases balance_bak > /data/bak
单表导出：mysqldump -uroot -proot balance_bak tower_cdr_prepare > /data/tower_cdr_prepare
整库导入：mysql -uroot -p < /data/balance_bak 
系统中导入表：mysql -uroot -proot balance_bak < /data/wx_account_gather          or    /data/wx_account_gather
}

语法： sed [-hnV][-e<script>][-f<script文件>][文本文件]

#调用sed命令有两种形式：  
*   sed [options] 'command' file(s)  
*   sed [options] -f scriptfile file(s)  

#参数说明：
-e<script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
-f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
-h或--help 显示帮助。
-n或--quiet或--silent 仅显示script处理后的结果。
-V或--version 显示版本信息。
#动作说明：
a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
p ：打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～
s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！例如 1,20s/old/new/g 就是啦！

【实例】

#在testfile文件的第四行后添加一行，并将结果输出到标准输出，在命令行提示符下输入如下命令：
sed -e 4a\newLine testfile 

#以行为单位的新增/删除
将 /etc/passwd 的内容列出并且列印行号，同时，请将第 2~5 行删除！
 nl /etc/passwd | sed '2,5d'     # 没有 -e 也行啦！同时也要注意的是， sed 后面接的动作，请务必以 '' 两个单引号括住喔！

只要删除第 2 行
nl /etc/passwd | sed '2d'

要删除第 3 到最后一行
nl /etc/passwd | sed '3,$d'

在第二行后(亦即是加在第三行)加上『drink tea?』字样！
sed -e '2a drint tea?' testtttt.txt 

那如果是要在第二行前
如果是要增加两行以上，在第二行后面加入两行字，例如 Drink tea or ..... 与 drink beer?
sed -e '2a drink tea? \n drink bear' testtttt.txt |nl

 nl testtttt.txt | sed '2i drint tea? or\  #命令行换行
drink bear?'
每一行之间都必须要以反斜杠『 \ 』来进行新行的添加喔！所以，上面的例子中，我们可以发现在第一行的最后面就有 \ 存在。

### 以行为单位的替换与显示
将第2-5行的内容取代成为『No 2-5 number』呢？
nl testtttt.txt | sed '2,5c no 2-5 number'

# 仅列出 /etc/passwd 文件内的第 5-7 行
nl testtttt.txt  | sed -n '2,5p' 

### 数据的搜寻并显示
搜索 /etc/passwd有root关键字的行
nl /etc/passwd | sed -n '/root/p'

###数据的搜寻并删除
删除/etc/passwd所有包含root的行，其他行输出
nl /etc/passwd | sed '/root/d' 

###数据的搜寻并执行命令
搜索/etc/passwd,找到root对应的行，执行后面花括号中的一组命令，每个命令之间用分号分隔，这里把bash替换为blueshell，再输出这行：
nl /etc/passwd | sed -n '/root/{s/bash/blueshell/;p;q}'     # 最后的q是退出

###数据的搜寻并替换
除了整行的处理模式之外， sed 还可以用行为单位进行部分数据的搜寻并取代。基本上 sed 的搜寻与替代的与 vi 相当的类似！他有点像这样：
sed 's/要被取代的字串/新的字串/g'
ifconfig |grep "inet 192"|sed 's/^.*inet//g' | sed 's/netma.*$//g' |nl -n rz -w 5 

### 多点编辑
一条sed命令，删除/etc/passwd第三行到末尾的数据，并把bash替换为blueshell
nl /etc/passwd | sed -e '3,$d' -e 's/bash/blueshell/'
-e表示多点编辑，第一个编辑命令删除/etc/passwd第三行到末尾的数据，第二条命令搜索bash替换为blueshell。

###直接修改文件内容(危险动作)
sed 可以直接修改文件的内容，不必使用管道命令或数据流重导向！ 不过，由於这个动作会直接修改到原始的文件，所以请你千万不要随便拿系统配置来测试！ 我们还是使用文件 regular_express.txt 文件来测试看看吧！

# 将 regular_express.txt 内每一行结尾若为 . 则换成 !
sed -i 's/\.$/\!/g' regular_express.txt

#利用 sed 直接在 regular_express.txt 最后一行加入 # This is a test:
利用 sed 直接在 regular_express.txt 最后一行加入 # This is a test:

由於 $ 代表的是最后一行，而 a 的动作是新增，因此该文件最后新增 # This is a test！

sed 的 -i 选项可以直接修改文件内容，这功能非常有帮助！举例来说，如果你有一个 100 万行的文件，你要在第 100 行加某些文字，此时使用 vim 可能会疯掉！因为文件太大了！那怎办？就利用 sed 啊！透过 sed 直接修改/取代的功能，你甚至不需要使用 vim 去修订！

### 插入空行
sed '1a \ \n\n\n\n\n\n\n\n\n' testtttt.txt | nl -b a  

```







### 虚拟机虚拟机硬盘扩容

```sql
https://blog.csdn.net/fuchen58/article/details/81172009?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0.base&spm=1001.2101.3001.4242

https://www.cnblogs.com/kerrycode/p/4423753.html

fdisk -l :打印当前的磁盘分区表，这时我们可以看到磁盘的总量
1 fdisk /dev/sda  
键入 ：m  "列出fdisk的帮助",
键入：n  " 命令n用于添加新分区" 
键入： p" 选择创建主分区"
直接回车选择默认值   最后要reboot
2 (创建逻辑分区-有时需要，有时不需要？)fdisk /dev/sda     依次键入：p n l p w  reboot
(格式化逻辑分区)mkfs.ext4 /dev/sda3

3. 挂载该分区： mkdir   /home/work
手动挂载，则键入：mount /dev/sda3 /home/work/   "表示将该新分区挂载到/home/work/这个目录下面"

4开机自动挂载，则修改/etc/fstab文件，在这个文件里面添加一行：
/dev/sda3       /home/work      ext4    defaults,        0     0
```



#### 虚拟机克隆后要改两处物理地址：00:50:56:2E:DD:B4

1 **MAC地址：/etc/udev/rules.d/70-persistent-net.rules**

**2 IP地址：**/etc/sysconfig/network-scripts/ifcfg-eno16777736



#### 修改主机名：

1临时命令格式：hostname  newhostname

2 通过配置文件/etc/sysconfig/network修改

3 改/etc下的hosts文件，在提示符下输入vi /etc/hosts    || 实际是：vim /etc/hostname

4 reboot

=================

报错：Failed to start Docker Application Container Engine

更新Linux的内核，输入命令 “ yum update ”  -- 升级操作系统，这个真解决了问题



#### zabbix连不上Mysql 连接错误，

```sql
1#### (98)address already in use: ah00072: make_sock: could not bind to address 0.0.0.0:80
问题描述：
80端口已经被占用，导致启动不了
解决思路：
一种是比较简单的情况，查看80端口进程号，然后kill -9 该进程号关闭占用该80端口的进程，然后重启即可
另一种是查询不到80端口被占用，但是出现这样的提示，我困惑很久，最后是参考该文得到的思路https://www.digitalocean.com/community/questions/98-address-already-in-use-ah00072-make_sock-could-not-bind-to-address-80-error
我的解决办法：
找到有可能配置的listen 80的配置文件（例如：nginx的配置文件等），看是否和/etc/httpd/conf/httpd.conf配置的有冲突，如果有，则需要需改其中一个即可解决。
总结：
其实这个问题并不是很大，但是容易忽略解决点，不要仅仅是看错误提示的字面意思；占用不一定是进程占用，还有可能是配置文件冲突导致的占用。
————————————————
版权声明：本文为CSDN博主「MobiusStrip」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/MobiusStrip/article/details/92847058


2##### [zabbix连不上数据库](https://www.cnblogs.com/seasonsstory/p/3209785.html)
日志查看: tail -f /var/log/zabbix/zabbix_server.log 
1267:20130722:195451.493 [Z3001] connection to database 'zabbix' failed: [2002] Can't' connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)
解决办法：
[root@localhost lib]# mkdir /var/lib/mysql
[root@localhost lib]# ln -s /tmp/mysql.sock /var/lib/mysql/mysql.sock
重启：service mysql restart

3####nginx httpd 都占用80端口 无法启动
vim /usr/local/nginx/conf/nginx.conf    listen=8080
启动：/usr/local/nginx/sbin/nginx
如果想停⽌Nginx服务，可执⾏：/usr/local/nginx/sbin/nginx -s stop
如果修改了配置⽂件后想重新加载Nginx，可执⾏：/usr/local/nginx/sbin/nginx -s reload

```

###  redis登陆

```sql
redis-cli  -c -h 172.29.106.9 -p 6379

redis-cli -p 6379 -a root123 # 使用密码端口登录命令
redis-cli         # 无密码端口登录命令
redis-cli -h host -p port -a password  # 在远程登录redis
```



### 改文件夹显示的颜色

![image-20211027160820226](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211027160820226.png)
