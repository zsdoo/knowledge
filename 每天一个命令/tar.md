正确：tar  zcvf   包名.tar.gz   源文件

### 针对单个文件，如果顺序反了的话，会造成文件消失

##### ！！！错误：tar  zcvf   源文件   包名.tar.gz   

-----

```sql
zcat xxx.tar.gz
zcat vsftpd.tar.gz|grep 'footbar.js'
tar tvf vsftpd.tar.gz

压缩：打包后，以gzip压缩 在参数f后面的压缩文件名是自己取的，习惯上用tar来做，
tar -zcvf test.tar.gz test 
解压：tar -zxvf /usr/local/test.tar.gz
```

gzip 保留源文件：

```sql
压缩：gzip 2wx_funds_detail_1014.sql  > 2wx_funds_detail_1014.sql.gz

解压：gzip -dc wx_funds_detail_1014.sql.gz > wx_funds_detail_1014.sql
```

总结

```bash
(1) *.tar 用 tar –xvf 解压
(2) *.gz 用 gzip -d或者gunzip 解压
(3) *.tar.gz和*.tgz 用 tar –xzf 解压
(4) *.bz2 用 bzip2 -d或者用bunzip2 解压
(5) *.tar.bz2用tar –xjf 解压
(6) *.Z 用 uncompress 解压
(7) *.tar.Z 用tar –xZf 解压
(8) *.rar 用 unrar e解压
(9) *.zip 用 unzip 解压
(10) *.xz 用 xz -d 解压
(11) *.tar.xz 用 tar -zJf 解压
```





## [linux下不解包查看tar包文件内容](https://www.cnblogs.com/Anidot/articles/7857696.html)

以下内容转自:http://www.361way.com/zcat-tar-zgrep/2550.html

为减少日志文件占用的空间，很多情况下我们会将日志文件以天或周为周期打包成tar.gz 包保存。虽然这样做有利空间充分利用，但当我们想查看压缩包内的内容时确很不方便。如果只是一个tar.gz文件，可以将其解压，再利用grep、awk或vi等工具查看或处理。不过如果有一个月或都一年的日志需要找出某些关键词的行，一个一个的解压，然后再看，是不是很不现实。那有没有什么简便的方法，可以不解压获得我们想要的内容呢？

答案是肯定的，可以利用zutils工具包实现。Zutils 是一组用来处理压缩文件的工具集，支持的压缩档包括：gzip, bzip2, lzip, and xz. 当前版本提供的命令有：zcat, zcmp, zdiff, and zgrep 。

直接查看tar.gz压缩包里的内容可以使用：

```bsh
zcat xxx.tar.gz

-- tar tvf vsftpd.tar.gz
```

 但是想要在其后面直接加管道grep处理呢？如下：

```bsh
[root@back tmp]# zgrep 'footbar.js' vsftpd.tar.gz
Binary file (standard input) matches
[root@back tmp]# zcat vsftpd.tar.gz|grep 'footbar.js'
Binary file (standard input) matches
```

发现不论是使用zgrep还是使用zcat后再grep都会报错。难道不行？当然不是。查看下zgrep或grep的帮助文档。有这么一行： 

```xml
--binary-files=text
```

 加上该参数呢？

```bsh
zcat vsftpd.tar.gz|grep --binary-files=text 'footbar.js'或
zgrep --binary-files=text 'footbar.js' vsftpd.tar.gz
```

 发现可以查看文件内容了 ! 为什么呢？

因为我压缩是用的tar czvf参数进行的打包。其实现上经过tar与gzip两层压缩。导致其直接不能管道。如果不解包想直接查看压缩包里包含了那些文件呢？可以用下面的命令：

```bsh
[root@back tmp]# tar tvf vsftpd.tar.gz
-rw------- root/root 441453365 2013-06-03 16:19:56 vsftpd.log
```



## [tar 解压缩命令详解](https://www.cnblogs.com/luozeng/p/8674529.html)

以下是对`tar`命令的一些总结：

```
1 # tar -cvf test.tar test 仅打包，不压缩 
2 # tar -zcvf test.tar.gz test 打包后，以gzip压缩 在参数f后面的压缩文件名是自己取的，习惯上用tar来做，如果加z参数，则以tar.gz 或tgz来代表gzip压缩过的tar file文件
```

解压操作:

```
1 #tar -zxvf /usr/local/test.tar.gz
```

tar 解压缩命令详解

```
1 -c: 建立压缩档案
2 -x：解压
3 -t：查看内容
4 -r：向压缩归档文件末尾追加文件
5 -u：更新原压缩包中的文件
```

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)

```
1 -z：有gzip属性的
2 -j：有bz2属性的
3 -J：具有xz属性的（注3）
4 -Z：有compress属性的
5 -v：显示所有过程
6 -O：将文件解开到标准输出
```

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)

下面的参数-f是必须的 
-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

```
1 # tar -cf all.tar *.jpg 
2 
3 # tar -rf all.tar *.gif 
```

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)

```
1 这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。
2 
3 # tar -uf all.tar logo.gif 
4 
5 
6 
7 这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。
8 
9 # tar -tf all.tar 
```

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)

```
 1 这条命令是列出all.tar包中所有文件，-t是列出文件的意思
 2 
 3 # tar -xf all.tar 
 4 这条命令是解出all.tar包中所有文件，-x是解开的意思
 5 
 6 压缩
 7 
 8 tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg
 9 tar –czf jpg.tar.gz *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz
10 tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2
11 tar –cZf jpg.tar.Z *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z
12 rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux
13 zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux
14 
15 
16 解压
17 
18 tar –xvf file.tar //解压 tar包
19 tar -xzvf file.tar.gz //解压tar.gz
20 tar -xjvf file.tar.bz2   //解压 tar.bz2
21 tar –xZvf file.tar.Z   //解压tar.Z
22 unrar e file.rar //解压rar
23 unzip file.zip //解压zip
```

[![复制代码](D:\工作文件\knowledge\总结\Knowledge_pictrue\copycode.gif)](javascript:void(0);)