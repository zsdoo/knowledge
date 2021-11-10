# docker启动关闭删除所有的容器命令

https://www.zhihu.com/people/ai-zhi-dao-da-an)

喜欢就关注吧，定期分享干货；

6 人赞同了该文章

1、启动所有容器

```text
docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)
```

2、关闭所有容器

```text
docker stop $(docker ps -a | awk '{ print $1}' | tail -n +2)
```

3、删除所有容器

```text
docker rm $(docker ps -a | awk '{ print $1}' | tail -n +2)
```

4、删除所有镜像（慎用）

```text
docker rmi $(docker images | awk '{print $3}' |tail -n +2)
```

备注：

![img](https://pic4.zhimg.com/80/v2-770019569928632deafc395c3c545b1b_1440w.jpg)



虚拟机克隆后要改两处物理地址：00:50:56:2E:DD:B4

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

### 宿主机无法连接docker中的mysql

```sql
因为是8.0要执行以下sql
alter user 'root'@'%' identified by '1234' password expire never;
alter user 'root'@'%' identified with mysql_native_password by '1234';
flush privileges;

安装mysql客户端
yum install mysql  -y


---

初始化后第一次使用数据库要修改密码：
#user mysql;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'abc11';

#授权允许远程访问
grant all privileges on *.* to 'root'@'%' identified by '@wjb13191835106';
flush privileges; 

#关闭授权
revoke all on *.* from dba@localhost;

```



```sql
mysql 中需要处理密码：

查看用户信息
select  host, user, authentication_string, plugin from mysql.user;

use mysql;

update user set host = '%' where user = 'root';

FLUSH PRIVILEGES;

 ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '1234';
```





#### 安装命令如下：

curl -fsSL https://get.docker.com | bash -s docker --mirror aliyun

卸载 docker
删除安装包：
yum remove docker-ce
删除镜像、容器、配置文件等内容：
rm -rf /var/lib/docker



启动命令如下

sudo systemctl enable docker # 开机自动启动docker

sudo systemctl start docker # 启动docker
sudo systemctl restart docker # 重启dokcer


-- -----------------------------------------


Docker 允许你在容器内运行应用程序， 使用 docker run 命令来在容器内运行一个应用程序。

#### 输出Hello world

```sql
runoob@runoob:~$ docker run ubuntu:15.10 /bin/echo "Hello world"
Hello world
```


各个参数解析：

```sql
docker: Docker 的二进制执行文件。
run: 与前面的 docker 组合来运行一个容器。
ubuntu:15.10 指定要运行的镜像，Docker 首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。
/bin/echo "Hello world": 在启动的容器里执行的命令
```

以上命令完整的意思可以解释为：Docker 以 ubuntu15.10 镜像创建一个新容器，然后在容器里执行 bin/echo "Hello world"，然后输出结果。

####  运行交互式的容器

我们通过 docker 的两个参数 -i -t，让 docker 运行的容器实现"对话"的能力：

```sql
runoob@runoob:~$ docker run -i -t ubuntu:15.10 /bin/bash
root@0123ce188bd8:/#
```

各个参数解析：

```bash
-t: 在新容器内指定一个伪终端或终端。
-i: 允许你对容器内的标准输入 (STDIN) 进行交互。
```

注意第二行 root@0123ce188bd8:/#，此时我们已进入一个 ubuntu15.10 系统的容器

我们尝试在容器中运行命令 cat /proc/version和ls分别查看当前系统的版本信息和当前目录下的文件列表

```shell
root@0123ce188bd8:/#  cat /proc/version
Linux version 4.4.0-151-generic (buildd@lgw01-amd64-043) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.10) ) #178-Ubuntu SMP Tue Jun 11 08:30:22 UTC 2019
root@0123ce188bd8:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@0123ce188bd8:/# 
```

我们可以通过运行 exit 命令或者使用 CTRL+D 来退出容器。

```shell
root@0123ce188bd8:/#  exit
exit
root@runoob:~# 
```

#### 启动容器（后台模式）

使用以下命令创建一个以进程方式运行的容器

```sql
runoob@runoob:~$ docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
2b1b7a428627c51ab8810d541d759f072b4fc75487eed05812646b8534a2fe63
```

在输出中，我们没有看到期望的 "hello world"，而是一串长字符

**2b1b7a428627c51ab8810d541d759f072b4fc75487eed05812646b8534a2fe63**

这个长字符串叫做容器 ID，对每个容器来说都是唯一的，我们可以通过容器 ID 来查看对应的容器发生了什么。

首先，我们需要确认容器有在运行，可以通过 **docker ps** 来查看：

```sql
runoob@runoob:~$ docker ps
CONTAINER ID        IMAGE                  COMMAND              ...  
5917eac21c36        ubuntu:15.10           "/bin/sh -c 'while t…"    ...
```

输出详情介绍：

**CONTAINER ID:** 容器 ID。

**IMAGE:** 使用的镜像。

**COMMAND:** 启动容器时运行的命令。

**CREATED:** 容器的创建时间。

**STATUS:** 容器状态。

状态有7种：

- created（已创建）
- restarting（重启中）
- running 或 Up（运行中）
- removing（迁移中）
- paused（暂停）
- exited（停止）
- dead（死亡）

**PORTS:** 容器的端口信息和使用的连接类型（tcp\udp）。

**NAMES:** 自动分配的容器名称。

在宿主主机内使用 **docker logs** 命令，查看容器内的标准输出：

```sql
runoob@runoob:~$ docker logs 2b1b7a428627

runoob@runoob:~$ docker logs amazing_cori
```

#### 停止容器

我们使用 **docker stop** 命令来停止容器:

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker25.png)

通过 **docker ps** 查看，容器已经停止工作:

```
runoob@runoob:~$ docker ps
```

可以看到容器已经不在了。

也可以用下面的命令来停止:

```
runoob@runoob:~$ docker stop amazing_cori
```

### Docker 容器使用



### *安装vim* 

sudo apt-get install vim

#### [Docker镜像的搜索下载以及查看删除操作](https://www.cnblogs.com/weisunblog/p/12233750.html)

查看本地镜像：docker images

搜索镜像：docker search centos

搜索镜像并过滤是官方的：docker search --filter "is-offical=true" centos

搜索镜像并过滤大于多少颗星的：docker search --filter stars=10 centos

下载centos7镜像：docker pull centos:7

修改本地镜像名字：docker tag centos:7 mycentos:1

本地镜像的删除：docker rmi centos:7

#### Docker 客户端

docker 客户端非常简单 ,我们可以直接输入 docker 命令来查看到 Docker 客户端的所有命令选项。

```
runoob@runoob:~# docker
```

#### 启动容器

以下命令使用 ubuntu 镜像启动一个容器，参数为以命令行模式进入该容器：

```
$ docker run -it ubuntu /bin/bash
```

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-container-run.png)

参数说明：

- **-i**: 交互式操作。
- **-t**: 终端。
- **ubuntu**: ubuntu 镜像。
- **/bin/bash**：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

要退出终端，直接输入 **exit**:

```
root@ed09e4490c57:/# exit
```

#### 启动已停止运行的容器

查看所有的容器命令如下：

```
$ docker ps -a
```

#### 后台运行

在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 **-d** 指定容器的运行模式。

```
$ docker run -itd --name ubuntu-test ubuntu /bin/bash
```

点击图片查看大图：

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-run-d.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-run-d.png)

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-run-d2.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-run-d2.png)

**注：**加了 **-d** 参数默认不会进入容器，想要进入容器需要使用指令 **docker exec**（下面会介绍到）。

#### 停止一个容器

停止容器的命令如下：

```
$ docker stop <容器 ID>
```

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-stop-1.png)

停止的容器可以通过 docker restart 重启：

```
$ docker restart <容器 ID>
```

#### 进入容器

在使用 **-d** 参数时，容器启动后会进入后台。此时想要进入容器，可以通过以下指令进入：

- **docker attach**
- **docker exec**：推荐大家使用 docker exec 命令，因为此退出容器终端，不会导致容器的停止。

**attach 命令**

下面演示了使用 docker attach 命令。

```
$ docker attach 1e560fca3906 
```

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-attach.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-attach.png)

**注意：** 如果从这个容器退出，会导致容器的停止。

**exec 命令**

下面演示了使用 docker exec 命令。

```
docker exec -it 243c32535da7 /bin/bash
```

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-exec.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-exec.png)

**注意：** 如果从这个容器退出，容器不会停止，这就是为什么推荐大家使用 **docker exec** 的原因。

更多参数说明请使用 **docker exec --help** 命令查看。

#### 导出和导入容器

#### **导出容器**

如果要导出本地某个容器，可以使用 **docker export** 命令。

```
$ docker export 1e560fca3906 > ubuntu.tar
```

导出容器 1e560fca3906 快照到本地文件 ubuntu.tar。

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-export.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-export.png)

这样将导出容器快照到本地文件。

#### **导入容器快照**

可以使用 docker import 从容器快照文件中再导入为镜像，以下实例将快照文件 ubuntu.tar 导入到镜像 test/ubuntu:v1:

```
$ cat docker/ubuntu.tar | docker import - test/ubuntu:v1
```

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-import.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-import.png)

此外，也可以通过指定 URL 或者某个目录来导入，例如：

```
$ docker import http://example.com/exampleimage.tgz example/imagerepo
```

#### 删除容器

删除容器使用 **docker rm** 命令：

```
$ docker rm -f 1e560fca3906
```

[![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-container-rmi.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-container-rmi.png)

下面的命令可以清理掉所有处于终止状态的容器。

$ docker container prune

### 运行一个 web 应用

前面我们运行的容器并没有一些什么特别的用处。

接下来让我们尝试使用 docker 构建一个 web 应用程序。

我们将在docker容器中运行一个 Python Flask 应用来运行一个web应用。

```
runoob@runoob:~# docker pull training/webapp  # 载入镜像
runoob@runoob:~# docker run -d -P training/webapp python app.py
```

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker29.png)

参数说明:

- **-d:**让容器在后台运行。
- **-P:**将容器内部使用的网络端口随机映射到我们使用的主机上。

#### 查看 WEB 应用容器

使用 docker ps 来查看我们正在运行的容器：

```
runoob@runoob:~#  docker ps
CONTAINER ID        IMAGE               COMMAND             ...        PORTS                 
d3d5e39ed9d3        training/webapp     "python app.py"     ...        0.0.0.0:32769->5000/tcp
```

这里多了端口信息。

```
PORTS
0.0.0.0:32769->5000/tcp
```

Docker 开放了 5000 端口（默认 Python Flask 端口）映射到主机端口 32769 上。

这时我们可以通过浏览器访问WEB应用

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker31.png)

我们也可以通过 -p 参数来设置不一样的端口：

```
runoob@runoob:~$ docker run -d -p 5000:5000 training/webapp python app.py
```

**docker ps**查看正在运行的容器

```
runoob@runoob:~#  docker ps
CONTAINER ID        IMAGE                             PORTS                     NAMES
bf08b7f2cd89        training/webapp     ...        0.0.0.0:5000->5000/tcp    wizardly_chandrasekhar
d3d5e39ed9d3        training/webapp     ...        0.0.0.0:32769->5000/tcp   xenodochial_hoov
```

容器内部的 5000 端口映射到我们本地主机的 5000 端口上。

------

#### 网络端口的快捷方式

通过 **docker ps** 命令可以查看到容器的端口映射，**docker** 还提供了另一个快捷方式 **docker port**，使用 **docker port** 可以查看指定 （ID 或者名字）容器的某个确定端口映射到宿主机的端口号。

上面我们创建的 web 应用容器 ID 为 **bf08b7f2cd89** 名字为 **wizardly_chandrasekhar**。

我可以使用 **docker port bf08b7f2cd89** 或 **docker port wizardly_chandrasekhar** 来查看容器端口的映射情况。

```
runoob@runoob:~$ docker port bf08b7f2cd89
5000/tcp -> 0.0.0.0:5000
runoob@runoob:~$ docker port wizardly_chandrasekhar
5000/tcp -> 0.0.0.0:5000
```

------

#### 查看 WEB 应用程序日志

docker logs [ID或者名字] 可以查看容器内部的标准输出。

```
runoob@runoob:~$ docker logs -f bf08b7f2cd89
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
192.168.239.1 - - [09/May/2016 16:30:37] "GET / HTTP/1.1" 200 -
192.168.239.1 - - [09/May/2016 16:30:37] "GET /favicon.ico HTTP/1.1" 404 -
```

**-f:** 让 **docker logs** 像使用 **tail -f** 一样来输出容器内部的标准输出。

从上面，我们可以看到应用程序使用的是 5000 端口并且能够查看到应用程序的访问日志。

------

#### 查看WEB应用程序容器的进程

我们还可以使用 docker top 来查看容器内部运行的进程

```
runoob@runoob:~$ docker top wizardly_chandrasekhar
UID     PID         PPID          ...       TIME                CMD
root    23245       23228         ...       00:00:00            python app.py
```

------

#### 检查 WEB 应用程序

使用 **docker inspect** 来查看 Docker 的底层信息。它会返回一个 JSON 文件记录着 Docker 容器的配置和状态信息。

```
runoob@runoob:~$ docker inspect wizardly_chandrasekhar
[
    {
        "Id": "bf08b7f2cd897b5964943134aa6d373e355c286db9b9885b1f60b6e8f82b2b85",
        "Created": "2018-09-17T01:41:26.174228707Z",
        "Path": "python",
        "Args": [
            "app.py"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 23245,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2018-09-17T01:41:26.494185806Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
......
```

------

#### 停止 WEB 应用容器

```
runoob@runoob:~$ docker stop wizardly_chandrasekhar   
wizardly_chandrasekhar
```

------

#### 重启WEB应用容器

已经停止的容器，我们可以使用命令 docker start 来启动。

```
runoob@runoob:~$ docker start wizardly_chandrasekhar
wizardly_chandrasekhar
```

docker ps -l 查询最后一次创建的容器：

```
#  docker ps -l 
CONTAINER ID        IMAGE                             PORTS                     NAMES
bf08b7f2cd89        training/webapp     ...        0.0.0.0:5000->5000/tcp    wizardly_chandrasekhar
```

正在运行的容器，我们可以使用 **docker restart** 命令来重启。

------

#### 移除WEB应用容器

我们可以使用 docker rm 命令来删除不需要的容器

```
runoob@runoob:~$ docker rm wizardly_chandrasekhar  
wizardly_chandrasekhar
```

删除容器时，容器必须是停止状态，否则会报如下错误

```
runoob@runoob:~$ docker rm wizardly_chandrasekhar
Error response from daemon: You cannot remove a running container bf08b7f2cd897b5964943134aa6d373e355c286db9b9885b1f60b6e8f82b2b85. Stop the container before attempting removal or force remove
```

### Docker 镜像使用

配置DOCKER镜像下载加速

```sql
vim /etc/docker/daemon.json

在其中加⼊加速镜像源地址即可：
{
 "registry-mirrors": ["http://hub-mirror.c.163.com"] 
}
 
 ⽐如这⾥使⽤的是 ⽹易 的加速源，其他像 阿⾥云 、 DaoCloud 这些也都提供加速源，按需选择即可。
加完加速地址后，重新加载配置⽂件，重启 docker 服务即可：
systemctl daemon-reload
systemctl restart docker.service
这样镜像加速器就配置完成了，后续下载 docker 镜像速度将⼤增。
```









当运行容器时，使用的镜像如果在本地中不存在，docker 就会自动从 docker 镜像仓库中下载，默认是从 Docker Hub 公共镜像源下载。

下面我们来学习：

- 1、管理和使用本地 Docker 主机镜像
- 2、创建镜像

------

#### 列出镜像列表

我们可以使用 **docker images** 来列出本地主机上的镜像。

```
runoob@runoob:~$ docker images           
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              14.04               90d5884b1ee0        5 days ago          188 MB
php                 5.6                 f40e9e0f10c8        9 days ago          444.8 MB
nginx               latest              6f8d099c3adc        12 days ago         182.7 MB
mysql               5.6                 f2e8d6c772c0        3 weeks ago         324.6 MB
httpd               latest              02ef73cf1bc0        3 weeks ago         194.4 MB
ubuntu              15.10               4e3b13c8a266        4 weeks ago         136.3 MB
hello-world         latest              690ed74de00f        6 months ago        960 B
training/webapp     latest              6fae60ef3446        11 months ago       348.8 MB
```

各个选项说明:

- **REPOSITORY：**表示镜像的仓库源
- **TAG：**镜像的标签
- **IMAGE ID：**镜像ID
- **CREATED：**镜像创建时间
- **SIZE：**镜像大小

同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，如 ubuntu 仓库源里，有 15.10、14.04 等多个不同的版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。

所以，我们如果要使用版本为15.10的ubuntu系统镜像来运行容器时，命令如下：

```
runoob@runoob:~$ docker run -t -i ubuntu:15.10 /bin/bash 
root@d77ccb2e5cca:/#
```

参数说明：

- **-i**: 交互式操作。
- **-t**: 终端。
- **ubuntu:15.10**: 这是指用 ubuntu 15.10 版本镜像为基础来启动容器。
- **/bin/bash**：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

如果要使用版本为 14.04 的 ubuntu 系统镜像来运行容器时，命令如下：

```
runoob@runoob:~$ docker run -t -i ubuntu:14.04 /bin/bash 
root@39e968165990:/# 
```

如果你不指定一个镜像的版本标签，例如你只使用 ubuntu，docker 将默认使用 ubuntu:latest 镜像。

#### 更新镜像

更新镜像之前，我们需要使用镜像来创建一个容器。

```
runoob@runoob:~$ docker run -t -i ubuntu:15.10 /bin/bash
root@e218edb10161:/# 
```

在运行的容器内使用 **apt-get update** 命令进行更新。

在完成操作之后，输入 exit 命令来退出这个容器。

此时 ID 为 e218edb10161 的容器，是按我们的需求更改的容器。我们可以通过命令 docker commit 来提交容器副本。

```
runoob@runoob:~$ docker commit -m="has update" -a="runoob" e218edb10161 runoob/ubuntu:v2
sha256:70bf1840fd7c0d2d8ef0a42a817eb29f854c1af8f7c59fc03ac7bdee9545aff8
```

各个参数说明：

- **-m:** 提交的描述信息
- **-a:** 指定镜像作者
- **e218edb10161：**容器 ID
- **runoob/ubuntu:v2:** 指定要创建的目标镜像名

我们可以使用 **docker images** 命令来查看我们的新镜像 **runoob/ubuntu:v2**：

```
runoob@runoob:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
runoob/ubuntu       v2                  70bf1840fd7c        15 seconds ago      158.5 MB
ubuntu              14.04               90d5884b1ee0        5 days ago          188 MB
php                 5.6                 f40e9e0f10c8        9 days ago          444.8 MB
nginx               latest              6f8d099c3adc        12 days ago         182.7 MB
mysql               5.6                 f2e8d6c772c0        3 weeks ago         324.6 MB
httpd               latest              02ef73cf1bc0        3 weeks ago         194.4 MB
ubuntu              15.10               4e3b13c8a266        4 weeks ago         136.3 MB
hello-world         latest              690ed74de00f        6 months ago        960 B
training/webapp     latest              6fae60ef3446        12 months ago       348.8 MB
```

使用我们的新镜像 **runoob/ubuntu** 来启动一个容器

```
runoob@runoob:~$ docker run -t -i runoob/ubuntu:v2 /bin/bash                            
root@1a9fbdeb5da3:/#
```

#### 构建镜像

我们使用命令 **docker build** ， 从零开始来创建一个新的镜像。为此，我们需要创建一个 Dockerfile 文件，其中包含一组指令来告诉 Docker 如何构建我们的镜像。

```
runoob@runoob:~$ cat Dockerfile 
FROM    centos:6.7
MAINTAINER      Fisher "fisher@sudops.com"

RUN     /bin/echo 'root:123456' |chpasswd
RUN     useradd runoob
RUN     /bin/echo 'runoob:123456' |chpasswd
RUN     /bin/echo -e "LANG=\"en_US.UTF-8\"" >/etc/default/local
EXPOSE  22
EXPOSE  80
CMD     /usr/sbin/sshd -D
```

每一个指令都会在镜像上创建一个新的层，每一个指令的前缀都必须是大写的。

第一条FROM，指定使用哪个镜像源

RUN 指令告诉docker 在镜像内执行命令，安装了什么。。。

然后，我们使用 Dockerfile 文件，通过 docker build 命令来构建一个镜像。

```
runoob@runoob:~$ docker build -t runoob/centos:6.7 .
Sending build context to Docker daemon 17.92 kB
Step 1 : FROM centos:6.7
 ---&gt; d95b5ca17cc3
Step 2 : MAINTAINER Fisher "fisher@sudops.com"
 ---&gt; Using cache
 ---&gt; 0c92299c6f03
Step 3 : RUN /bin/echo 'root:123456' |chpasswd
 ---&gt; Using cache
 ---&gt; 0397ce2fbd0a
Step 4 : RUN useradd runoob
......
```

参数说明：

- **-t** ：指定要创建的目标镜像名
- **.** ：Dockerfile 文件所在目录，可以指定Dockerfile 的绝对路径

使用docker images 查看创建的镜像已经在列表中存在,镜像ID为860c279d2fec

```
runoob@runoob:~$ docker images 
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
runoob/centos       6.7                 860c279d2fec        About a minute ago   190.6 MB
runoob/ubuntu       v2                  70bf1840fd7c        17 hours ago         158.5 MB
ubuntu              14.04               90d5884b1ee0        6 days ago           188 MB
php                 5.6                 f40e9e0f10c8        10 days ago          444.8 MB
nginx               latest              6f8d099c3adc        12 days ago          182.7 MB
mysql               5.6                 f2e8d6c772c0        3 weeks ago          324.6 MB
httpd               latest              02ef73cf1bc0        3 weeks ago          194.4 MB
ubuntu              15.10               4e3b13c8a266        5 weeks ago          136.3 MB
hello-world         latest              690ed74de00f        6 months ago         960 B
centos              6.7                 d95b5ca17cc3        6 months ago         190.6 MB
training/webapp     latest              6fae60ef3446        12 months ago        348.8 MB
```

我们可以使用新的镜像来创建容器

```
runoob@runoob:~$ docker run -t -i runoob/centos:6.7  /bin/bash
[root@41c28d18b5fb /]# id runoob
uid=500(runoob) gid=500(runoob) groups=500(runoob)
```

从上面看到新镜像已经包含我们创建的用户 runoob。

#### 设置镜像标签

我们可以使用 docker tag 命令，为镜像添加一个新的标签。

```
runoob@runoob:~$ docker tag 860c279d2fec runoob/centos:dev
```

docker tag 镜像ID，这里是 860c279d2fec ,用户名称、镜像源名(repository name)和新的标签名(tag)。

使用 docker images 命令可以看到，ID为860c279d2fec的镜像多一个标签。

```
runoob@runoob:~$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
runoob/centos       6.7                 860c279d2fec        5 hours ago         190.6 MB
runoob/centos       dev                 860c279d2fec        5 hours ago         190.6 MB
runoob/ubuntu       v2                  70bf1840fd7c        22 hours ago        158.5 MB
ubuntu              14.04               90d5884b1ee0        6 days ago          188 MB
php                 5.6                 f40e9e0f10c8        10 days ago         444.8 MB
nginx               latest              6f8d099c3adc        13 days ago         182.7 MB
mysql               5.6                 f2e8d6c772c0        3 weeks ago         324.6 MB
httpd               latest              02ef73cf1bc0        3 weeks ago         194.4 MB
ubuntu              15.10               4e3b13c8a266        5 weeks ago         136.3 MB
hello-world         latest              690ed74de00f        6 months ago        960 B
centos              6.7                 d95b5ca17cc3        6 months ago        190.6 MB
training/webapp     latest              6fae60ef3446  
```

## Docker 容器连接

前面我们实现了通过网络端口来访问运行在 docker 容器内的服务。

容器中可以运行一些网络应用，要让外部也可以访问这些应用，可以通过 **-P** 或 **-p** 参数来指定端口映射。

下面我们来实现通过端口连接到一个 docker 容器。

------

#### 网络端口映射

我们创建了一个 python 应用的容器。

```
runoob@runoob:~$ docker run -d -P training/webapp python app.py
fce072cc88cee71b1cdceb57c2821d054a4a59f67da6b416fceb5593f059fc6d
```

另外，我们可以指定容器绑定的网络地址，比如绑定 127.0.0.1。

我们使用 **-P** 绑定端口号，使用 **docker ps** 可以看到容器端口 5000 绑定主机端口 32768。

```
runoob@runoob:~$ docker ps
CONTAINER ID    IMAGE               COMMAND            ...           PORTS                     NAMES
fce072cc88ce    training/webapp     "python app.py"    ...     0.0.0.0:32768->5000/tcp   grave_hopper
```

我们也可以使用 **-p** 标识来指定容器端口绑定到主机端口。

两种方式的区别是:

- **-P :**是容器内部端口**随机**映射到主机的高端口。
- **-p :** 是容器内部端口绑定到**指定**的主机端口。

```
runoob@runoob:~$ docker run -d -p 5000:5000 training/webapp python app.py
33e4523d30aaf0258915c368e66e03b49535de0ef20317d3f639d40222ba6bc0
runoob@runoob:~$ docker ps
CONTAINER ID        IMAGE               COMMAND           ...           PORTS                     NAMES
33e4523d30aa        training/webapp     "python app.py"   ...   0.0.0.0:5000->5000/tcp    berserk_bartik
fce072cc88ce        training/webapp     "python app.py"   ...   0.0.0.0:32768->5000/tcp   grave_hopper
```

另外，我们可以指定容器绑定的网络地址，比如绑定 127.0.0.1。

```
runoob@runoob:~$ docker run -d -p 127.0.0.1:5001:5000 training/webapp python app.py
95c6ceef88ca3e71eaf303c2833fd6701d8d1b2572b5613b5a932dfdfe8a857c
runoob@runoob:~$ docker ps
CONTAINER ID        IMAGE               COMMAND           ...     PORTS                                NAMES
95c6ceef88ca        training/webapp     "python app.py"   ...  5000/tcp, 127.0.0.1:5001->5000/tcp   adoring_stonebraker
33e4523d30aa        training/webapp     "python app.py"   ...  0.0.0.0:5000->5000/tcp               berserk_bartik
fce072cc88ce        training/webapp     "python app.py"   ...    0.0.0.0:32768->5000/tcp              grave_hopper
```

这样我们就可以通过访问 127.0.0.1:5001 来访问容器的 5000 端口。

上面的例子中，默认都是绑定 tcp 端口，如果要绑定 UDP 端口，可以在端口后面加上 **/udp**。

```
runoob@runoob:~$ docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py
6779686f06f6204579c1d655dd8b2b31e8e809b245a97b2d3a8e35abe9dcd22a
runoob@runoob:~$ docker ps
CONTAINER ID        IMAGE               COMMAND           ...   PORTS                                NAMES
6779686f06f6        training/webapp     "python app.py"   ...   5000/tcp, 127.0.0.1:5000->5000/udp   drunk_visvesvaraya
95c6ceef88ca        training/webapp     "python app.py"   ...    5000/tcp, 127.0.0.1:5001->5000/tcp   adoring_stonebraker
33e4523d30aa        training/webapp     "python app.py"   ...     0.0.0.0:5000->5000/tcp               berserk_bartik
fce072cc88ce        training/webapp     "python app.py"   ...    0.0.0.0:32768->5000/tcp              grave_hopper
```

**docker port** 命令可以让我们快捷地查看端口的绑定情况。

```
runoob@runoob:~$ docker port adoring_stonebraker 5000
127.0.0.1:5001
```

## Docker 容器互联

端口映射并不是唯一把 docker 连接到另一个容器的方法。

docker 有一个连接系统允许将多个容器连接在一起，共享连接信息。

docker 连接会创建一个父子关系，其中父容器可以看到子容器的信息。

------

### 容器命名

当我们创建一个容器的时候，docker 会自动对它进行命名。另外，我们也可以使用 **--name** 标识来命名容器，例如：

```
runoob@runoob:~$  docker run -d -P --name runoob training/webapp python app.py
43780a6eabaaf14e590b6e849235c75f3012995403f97749775e38436db9a441
```

我们可以使用 **docker ps** 命令来查看容器名称。

```
runoob@runoob:~$ docker ps -l
CONTAINER ID     IMAGE            COMMAND           ...    PORTS                     NAMES
43780a6eabaa     training/webapp   "python app.py"  ...     0.0.0.0:32769->5000/tcp   runoob
```

#### 新建网络

下面先创建一个新的 Docker 网络。

```
$ docker network create -d bridge test-net
```

![img](https://www.runoob.com/wp-content/uploads/2016/05/docker-net.png)

参数说明：

**-d**：参数指定 Docker 网络类型，有 bridge、overlay。

其中 overlay 网络类型用于 Swarm mode，在本小节中你可以忽略它。





# mysql-proxy

docker 创建JDK容器：docker run -it -v /root/java:/root/java openjdk  bash

[^]: -v 宿主机地址：容器地址

​	

docker 导出镜像：docker save -o /root/openjdk.tar.gz openjdk

docker 导入镜像： docker load < /root/openjdk.tar.gz

镜像改名：docker tag openjdk openjdk1

![image-20210808204947431](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808204947431.png)

完整创建java容器：docker run -it --name java -p 9000:8080 -v /root/java/:/root/java --privileged openjdk bash

容器暂停与恢复：docker pause java    	docker unpause java



![image-20210808210812746](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808210812746.png)

#### 创建与解散

```bash
docker swarm init
docker swarm leave -f

查看pxc集群信息：
docker exec pn1 ps -ef
```



#### 打开某个端口并应用 开户防火墙端口

```bash
[root@hecs-200776 ~]# firewall-cmd --zone=public --add-port=2377/tcp --permanent
success
[root@hecs-200776 ~]# firewall-cmd --reload
success


开户防火墙端口
firewall-cmd --zone=public --add-port=2377/tcp --permanetn
firewall-cmd --zone=public --add-port=7946/tcp --permanetn
firewall-cmd --zone=public --add-port=7946/udp --permanetn
firewall-cmd --zone=public --add-port=4789/tcp --permanetn
firewall-cmd --zone=public --add-port=4789/udp --permanetn
firewall-cmd --reload
```



集群初始化

```bash
[root@hecs-200776 ~]# docker swarm init
Swarm initialized: current node (9ztdi3nsl8ltav39cfisw7fa4) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-27k5h5algfqf90rksfjvnpxtba4rqmkdtgs8108i33128z5v1b-7ojegbvrngk20jofeowcwn0xp 192.168.0.120:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

```
https://www.cnblogs.com/zhujingzhi/p/9792432.html

# 在次执行上面的命令，回报下面的错误
[root@manager43 ~]``# docker swarm init --advertise-addr 192.168.31.43
Error response from daemon: This node is already part of a swarm. Use ``"docker swarm leave"` `to leave this swarm and ``join` `another one.
# 解决方法
[root@manager43 ~]``# docker swarm leave -f
这里的leave就是在集群中删除节点，-f参数强制删除，执行完在重新执行OK
```

#### 重新获取token

docker swarm join-token manager

docker swarm join --token SWMTKN-1-1juwgedde2npaet9yzw2we9abwhcqc93biwyezcytqmeubadk4-7qiaxavnsor7eit57zyslvuex 119.3.91.15:2377 

 docker swarm join --token SWMTKN-1-07x4myeqskfmvwcjulcp6lkxh9r6m064p28zt1cjkkw06ncfxu-2vx1tcy3r7slaq52pkbwx9j54 119.3.91.15:2377

![image-20210808212004428](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808212004428.png)

![image-20210808213710719](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808213710719.png)

![image-20210808213805361](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808213805361.png)

#### 创建虚拟网络

```sql

[root@hecs-200776 ~]# docker network create -d overlay --attachable swarm_mysql
a0agmb8kh4fsvf5ruz51u0bby
[root@hecs-200776 ~]# docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
7524557581f3   bridge            bridge    local
a2ab52480b62   docker_gwbridge   bridge    local
11923e1577a4   host              host      local
x3ga91g2wmcp   ingress           overlay   swarm
b0ae7eb1941a   none              null      local
a0agmb8kh4fs   swarm_mysql       overlay   swarm
2019c293f896   test-net          bridge    local

-- 删除虚拟网络
[root@hecs-200776 ~]# docker network rm swarm_mysql 
```

![image-20210808214329760](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808214329760.png)

![image-20210808215035834](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808215035834.png)

```sql
必须要开启防火墙端口
每个虚拟机节点都要开放Swarm集群的三个端口，reload防火墙之后，还要重启每个节点的Docker服务，然后才能创建PXC容器，否则就会出现因为防火墙的原因，导致从节点无法连接主节点容器。

firewall-cmd --zone=public --add-port=2377/tcp --permanent
firewall-cmd --zone=public --add-port=7946/tcp --permanent
firewall-cmd --zone=public --add-port=7946/udp --permanent
firewall-cmd --zone=public --add-port=4789/tcp --permanent
firewall-cmd --zone=public --add-port=4789/udp --permanent
firewall-cmd --reload
```



## 下载PXC镜像并搭建

第一个集群

| 虚拟机  | IP地址          | 端口 | 容器   | 数据卷 |
| ------- | --------------- | ---- | ------ | ------ |
| 虚拟机1 | 192.168.199.131 | 9001 | pn1(M) | pnv1   |
| 虚拟机2 | 192.168.199.132 | 9001 | pn2(S) | pnv2   |
| 虚拟机3 | 192.168.199.133 | 9001 | pn3(S) | pnv3   |
| 虚拟机4 |                 |      |        |        |



第二个集群

| 虚拟机  | IP地址          | 端口 | 容器   | 数据卷 |
| ------- | --------------- | ---- | ------ | ------ |
| 虚拟机1 | 192.168.199.131 | 9002 | pn1(M) | pnv5   |
| 虚拟机2 | 192.168.199.132 | 9002 | pn2(S) | pnv6   |
| 虚拟机3 | 192.168.199.133 | 9002 | pn3(S) | pnv7   |
| 虚拟机4 |                 |      |        |        |

![image-20210808215747221](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808215747221.png)

#### 建议下载5.7.21版本的PXC镜像

```bash
很多同学反馈说下载的PXC镜像，搭建集群的时候会出现问题。所以我建议各位同学下载5.7.21版本的PXC镜像。

docker pull percona/percona-xtradb-cluster:5.7.21
docker tag percona/percona-xtradb-cluster:5.7.21 pxc
docker rmi percona/percona-xtradb-cluster:5.7.21


#### 打包镜像：docker save pxc -o pxc.tar.gz   --打包到当前目录

#### 导入镜像 docker load -i pxc.tar.gz
```

![image-20210808221939785](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808221939785.png)



![image-20210808222003057](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808222003057.png)

![image-20210808222314860](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808222314860.png)

#### 创建主节点

```bash
[root@hecs-200776 ~]# docker run -d -p 9001:3306 -e MYSQL_ROOT_PASSWORD=abc123 -e CLUSTER_NAME=PXC2 -e XTRABACKUP_PASSWORK=abc123 -v pnv1:/var/lib/mysql --privileged --name pn1 --net=swarm_mysql pxc
63e599c48cba1b34bcd49bd1bf5bae180252cff2d41b348308f439f155d6681b
[root@hecs-200776 ~]# 

!!! 第三次成功。并且密码变的和主机密码一样
```

![image-20210808222728270](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210808222728270.png)

#### 创建从节点

```sql
[root@hecs-200776 ~]# docker run -d -p 9001:3306 -e MYSQL_ROOT_PASSWORD=abc123 -e CLUSTER_NAME=PXC2 -e XTRABACKUP_PASSWORK=abc123 -e CLUSTER_JOIN=pn1 -v pnv2:/var/lib/mysql --privileged --name pn2 --net=swarm_mysql pxc
63e599c48cba1b34bcd49bd1bf5bae180252cff2d41b348308f439f155d6681b

docker run -d -p 9001:3306 -e MYSQL_ROOT_PASSWORD=abc123 -e CLUSTER_NAME=PXC2 -e XTRABACKUP_PASSWORK=abc123 -e CLUSTER_JOIN=pn1 -v pnv3:/var/lib/mysql --privileged --name pn3 --net=swarm_mysql pxc

docker run -d -p 9001:3306 -e MYSQL_ROOT_PASSWORD=abc123 -e CLUSTER_NAME=PXC2 -e XTRABACKUP_PASSWORK=abc123 -e CLUSTER_JOIN=pn1 -v pnv4:/var/lib/mysql --privileged --name pn4 --net=swarm_mysql pxc

docker run -d -p 9001:3306 -e MYSQL_ROOT_PASSWORD=abc123 -e CLUSTER_NAME=PXC2 -e XTRABACKUP_PASSWORK=abc123 -e CLUSTER_JOIN=pn2 -v pnv4:/var/lib/mysql --privileged --name pn1 --net=swarm_mysql pxc
```

##### 由于 意外宕机docker start pxc节点后闪退，解决方法如下(未解决，参考下)

```sql
1.依次找出数据卷映射目录，修改参数
docker inspect v1
[
    {
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/v1/_data",
        "Name": "v1",
        "Options": {},
        "Scope": "local"
    }
]
2.修改配置文件
cd到目录下
vi grastate.dat 
safe_to_bootstrap设置成1
```

##### 在一个创建中创建PXC同样失败

```bash
可再试试

-- docker volume create pnv11 
docker run -d -p 9011:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -e XTRABACKUP_PASSWORK=abc11 -v pnv11:/var/lib/mysql11 --privileged --name pn11 pxc


-- docker volume create pnv12
docker run -d -p 9012:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -e XTRABACKUP_PASSWORK=abc11 -e CLUSTER_JOIN=pn11 -v pnv12:/var/lib/mysql12 --privileged --name pn12 pxc

-- 查看位置
[root@hecs-200776 _data]# docker volume inspect pnv12
[
    {
        "CreatedAt": "2021-08-09T17:50:01+08:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/pnv12/_data",
        "Name": "pnv12",
        "Options": {},
        "Scope": "local"
    }
]
```

##### 最终成功：

```bash
创建一个网络：docker network create pxc-network
去掉两个选项后成功：-e XTRABACKUP_PASSWORK=abc11  --privileged

  docker network create pxc-network
  docker volume create pnv11
  docker volume create pnv12
  docker volume create pnv13
  docker volume create pnv14
要修改: -p  -v  --name
docker run -d -p 9011:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -v pnv11:/var/lib/mysql11 --name=pn11 --net=pxc-network pxc

docker run -d -p 9012:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -e CLUSTER_JOIN=pn11 -v pnv12:/var/lib/mysql12 --name=pn12 --net=pxc-network  pxc

docker run -d -p 9013:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -e CLUSTER_JOIN=pn11 -v pnv13:/var/lib/mysql13 --name=pn13 --net=pxc-network  pxc

docker run -d -p 9014:3306 -e MYSQL_ROOT_PASSWORD=abc11 -e CLUSTER_NAME=PXC11 -e CLUSTER_JOIN=pn11 -v pnv13:/var/lib/mysql14 --name=pn14 --net=pxc-network  pxc
```







部分命令

```sql
docker inspect [OPTIONS] NAME|ID [NAME|ID...]

# 查看redis:latest镜像信息
docker inspect --type=image pxc
#查看目录挂载信息
docker inspect --format="{{json .Mounts}}" pn1
docker inspect --format="{{json .Mounts}}" pn1
#使用python的json模块美化
 
docker inspect --format="{{json .Mounts}}" container | python -m json.tool
 
#使用jq美化
 
docker inspect --format="{{json .Mounts}}" pn1 | jq

#查看完整网络信息
 
docker inspect --format="{{json .NetworkSettings}}" pn1 | jq
 
#查看网络端口映射
 
docker inspect --format="{{json .NetworkSettings.Ports}}" pn1 | jq
 
# 查看容器的网络ip、网关等信息
 
docker inspect --format="{{json .NetworkSettings.Networks}}" pn1 | jq

```

**grastate.dat**

**把此文件删除后，重新启动容器。**

或：

### 2.修改配置文件

cd到目录下
vi grastate.dat 
safe_to_bootstrap设置成1    -- 用这个方法依次起用容器成功， 



https://www.jianshu.com/p/7246448d4c4e?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation



# my29_PXC集群状态查看

**节点从集群中移除的状态**

show status like '%wsrep%';
wsrep_cluster_status为Disconnected则表示该节点已经不在集群中了，示例如下

```
> show status like '%wsrep%';
+--------------------------+----------------------+
| Variable_name            | Value                |
+--------------------------+----------------------+
| wsrep_cluster_conf_id    | 18446744073709551615 |
| wsrep_cluster_size       | 0                    |
| wsrep_cluster_state_uuid |                      |
| wsrep_cluster_status     | Disconnected         |
| wsrep_connected          | OFF                  |
| wsrep_local_bf_aborts    | 0                    |
| wsrep_local_index        | 18446744073709551615 |
| wsrep_provider_name      |                      |
| wsrep_provider_vendor    |                      |
| wsrep_provider_version   |                      |
| wsrep_ready              | ON                   |
+--------------------------+----------------------+
11 rows in set (0.00 sec)
```

**正常的集群节点状态**

```
>show status like '%wsrep%';
+----------------------------------+-----------------------------------------------------+
| Variable_name                    | Value                                               |
+----------------------------------+-----------------------------------------------------+
| wsrep_local_state_uuid           | 5a290219-fcfc-11e8-b8b9-13c62e5c16f1                |
| wsrep_protocol_version           | 8                                                   |
| wsrep_last_applied               | 6611991575                                          |
| wsrep_last_committed             | 6611991589                                          |
| wsrep_replicated                 | 524590452                                           |
| wsrep_replicated_bytes           | 1094596990048                                       |
| wsrep_repl_keys                  | 5967904705                                          |
| wsrep_repl_keys_bytes            | 60340440512                                         |
| wsrep_repl_data_bytes            | 998666384164                                        |
| wsrep_repl_other_bytes           | 0                                                   |
| wsrep_received                   | 3695397                                             |
| wsrep_received_bytes             | 29564596                                            |
| wsrep_local_commits              | 524590438                                           |
| wsrep_local_cert_failures        | 0                                                   |
| wsrep_local_replays              | 0                                                   |
| wsrep_local_send_queue           | 0                                                   |
| wsrep_local_send_queue_max       | 66                                                  |
| wsrep_local_send_queue_min       | 0                                                   |
| wsrep_local_send_queue_avg       | 2.321160                                            |
| wsrep_local_recv_queue           | 0                                                   |
| wsrep_local_recv_queue_max       | 3                                                   |
| wsrep_local_recv_queue_min       | 0                                                   |
| wsrep_local_recv_queue_avg       | 0.000160                                            |
| wsrep_local_cached_downto        | 6605892261                                          |
| wsrep_flow_control_paused_ns     | 173078420690665                                     |
| wsrep_flow_control_paused        | 0.164600                                            |
| wsrep_flow_control_sent          | 0                                                   |
| wsrep_flow_control_recv          | 2806150                                             |
| wsrep_flow_control_interval      | [ 141, 141 ]                                        |
| wsrep_flow_control_interval_low  | 141                                                 |
| wsrep_flow_control_interval_high | 141                                                 |
| wsrep_flow_control_status        | OFF                                                 |
| wsrep_cert_deps_distance         | 418.873157                                          |
| wsrep_apply_oooe                 | 0.723585                                            |
| wsrep_apply_oool                 | 0.047621                                            |
| wsrep_apply_window               | 3.941686                                            |
| wsrep_commit_oooe                | 0.000000                                            |
| wsrep_commit_oool                | 0.000000                                            |
| wsrep_commit_window              | 1.047392                                            |
| wsrep_local_state                | 4                                                   |
| wsrep_local_state_comment        | Synced                                              |
| wsrep_cert_index_size            | 468                                                 |
| wsrep_cert_bucket_count          | 520252                                              |
| wsrep_gcache_pool_size           | 4294968600                                          |
| wsrep_causal_reads               | 0                                                   |
| wsrep_cert_interval              | 9.885857                                            |
| wsrep_ist_receive_status         |                                                     |
| wsrep_ist_receive_seqno_start    | 0                                                   |
| wsrep_ist_receive_seqno_current  | 0                                                   |
| wsrep_ist_receive_seqno_end      | 0                                                   |
| wsrep_incoming_addresses         | 10.*.*.*:3306,10.*.*.*:3306             |
| wsrep_desync_count               | 0                                                   |
| wsrep_evs_delayed                |                                                     |
| wsrep_evs_evict_list             |                                                     |
| wsrep_evs_repl_latency           | 0.000125601/0.000556424/0.00157762/0.000167964/6997 |
| wsrep_evs_state                  | OPERATIONAL                                         |
| wsrep_gcomm_uuid                 | e52417ca-fcf6-11e8-ad11-12b1aba37990                |
| wsrep_cluster_conf_id            | 4                                                   |
| wsrep_cluster_size               | 2                                                   |
| wsrep_cluster_state_uuid         | 5a290219-fcfc-11e8-b8b9-13c62e5c16f1                |
| wsrep_cluster_status             | Primary                                             |
| wsrep_connected                  | ON                                                  |
| wsrep_local_bf_aborts            | 0                                                   |
| wsrep_local_index                | 1                                                   |
| wsrep_provider_name              | Galera                                              |
| wsrep_provider_vendor            | Codership Oy <info@codership.com>                   |
| wsrep_provider_version           | 3.26(rac090bc)                                      |
| wsrep_ready                      | ON                                                  |
+----------------------------------+-----------------------------------------------------+
68 rows in set (0.04 sec)
```

**主要参数说明**

该集群原来是三个节点，一个节点从集群移出之后，wsrep_incoming_addresses 显示为了两个节点；

wsrep_cluster_status 在所在正常的节点中都显示为Primary ，显示为其他值时表示节点有异常

wsrep_flow_control_paused表示复制停止了多少秒

 

**监控状态说明**
集群完整性检查:
wsrep_cluster_state_uuid:在集群所有节点的值应该是相同的,有不同值的节点,说明其没有连接入集群.
wsrep_cluster_conf_id:正常情况下所有节点上该值是一样的.如果值不同,说明该节点被临时”分区”了.当节点之间网络连接恢复 的时候应该会恢复一样的值.
wsrep_cluster_size:如果这个值跟预期的节点数一致,则所有的集群节点已经连接.
wsrep_cluster_status:集群组成的状态.如果不为”Primary”,说明出现”分区”或是”split-brain”脑裂状况.

节点状态检查:
wsrep_ready: 该值为 ON,则说明可以接受 SQL 负载.如果为 Off,则需要检查 wsrep_connected.
wsrep_connected: 如果该值为 Off,且 wsrep_ready 的值也为 Off,则说明该节点没有连接到集群.(可能是 wsrep_cluster_address 或 wsrep_cluster_name 等配置错造成的.具体错误需要查看错误日志)
wsrep_local_state_comment:如果 wsrep_connected 为 On,但 wsrep_ready 为 OFF,则可以从该项查看原因.

复制健康检查:
wsrep_flow_control_paused:表示复制停止了多长时间.即表明集群因为 Slave 延迟而慢的程度.值为 0~1,越靠近 0 越好,值为 1 表示 复制完全停止.可优化 wsrep_slave_threads 的值来改善.

wsrep_cert_deps_distance:有多少事务可以并行应用处理.wsrep_slave_threads 设置的值不应该高出该值太多. 

*wsrep_flow_control_sent:表示该节点已经停止复制了多少次.
wsrep_local_recv_queue_avg:表示 slave 事务队列的平均长度.slave 瓶颈的预兆.
最慢的节点的 wsrep_flow_control_sent 和 wsrep_local_recv_queue_avg 这两个值最高.这两个值较低的话,相对更好.*

检测慢网络问题:
wsrep_local_send_queue_avg:网络瓶颈的预兆.如果这个值比较高的话,可能存在网络瓶

冲突或死锁的数目:
wsrep_last_committed:最后提交的事务数目
wsrep_local_cert_failures 和 wsrep_local_bf_aborts:回滚,检测到的冲突数目



###  慕客9-6 管理Docker数据卷

-- 数据卷相当于给容器挂载一个虚拟的磁盘
docker volume ls # 数据卷列表
docker volume create test  #创建数据卷
docker volume rm test  # 删除数据卷
docker volume prune  # 清除没有挂载的数据卷
docker volume inspect pnv1 # 查看数据卷详情



#### 容器启动注意事项

cat grastate.dat 

safe_to_bootstrap: 1 (主节点)， 关闭时要最后关闭主节点，启动时要最先启动。

如果主节点退出，要删掉容器，将值改为0，再以从节点的身份启动。



## 创建Replication集群



- Replication集群是MySQL自带的数据同步机制
- MySQL通过读取、执行另一个MySQL的bin_log日志，实现数据同步

#### 5.4.1 下载Replication镜像

```shell
docker pull mishamx/mysql   
docker tag mishamx/mysql rep
docker rmi mishamx/mysql
```

#### 5.4.2 创建主节点

```shell
docker run -d -p 9003:3306 --name rn1 -e MYSQL_MASTER_PORT=3306 -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_REPLICATION_USER=backup -e MYSQL_REPLICATION_PASSWORD=backup123 -v rnv1:/var/lib/mysql --privileged --net=swarm_mysql rep
```

#### 5.4.3 创建从节点

```shell
docker run -d -p 9003:3306 --name rn2 -e MYSQL_MASTER_HOST=rn1 -e MYSQL_MASTER_PORT=3306 -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_REPLICATION_USER=backup -e MYSQL_REPLICATION_PASSWORD=backup123 -v rnv2:/var/lib/mysql --privileged --net=swarm_mysql rep
```

#### 5.4.4 创建两个Replication集群

第一个分片

| 虚拟机  | IP地址          | 端口 | 容器   | 数据卷 |
| ------- | --------------- | ---- | ------ | ------ |
| 虚拟机1 | 192.168.199.131 | 9003 | rn1(M) | rnv1   |
| 虚拟机2 | 192.168.199.132 | 9003 | rn2(S) | rnv2   |
| 虚拟机3 | 192.168.199.133 | 9003 | rn3(S) | rnv3   |
| 虚拟机4 |                 |      |        |        |

第二个分片

```sql
docker run -d -p 9004:3306 --name rn5 -e MYSQL_MASTER_PORT=3306 -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_REPLICATION_USER=backup -e MYSQL_REPLICATION_PASSWORD=backup123 -v rnv5:/var/lib/mysql --privileged --net=swarm_mysql rep

docker run -d -p 9004:3306 --name rn6 -e MYSQL_MASTER_HOST=rn5 -e MYSQL_MASTER_PORT=3306 -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_REPLICATION_USER=backup -e MYSQL_REPLICATION_PASSWORD=backup123 -v rnv6:/var/lib/mysql --privileged --net=swarm_mysql rep

docker run -d -p 9004:3306 --name rn7 -e MYSQL_MASTER_HOST=rn5 -e MYSQL_MASTER_PORT=3306 -e MYSQL_ROOT_PASSWORD=abc123 -e MYSQL_REPLICATION_USER=backup -e MYSQL_REPLICATION_PASSWORD=backup123 -v rnv7:/var/lib/mysql --privileged --net=swarm_mysql rep
```



| 虚拟机  | IP地址          | 端口 | 容器   | 数据卷 |
| ------- | --------------- | ---- | ------ | ------ |
| 虚拟机1 | 192.168.199.131 | 9004 | rn5(M) | rnv5   |
| 虚拟机2 | 192.168.199.132 | 9004 | rn6(S) | rnv6   |
| 虚拟机3 | 192.168.199.133 | 9004 | rn7(S) | rnv7   |
| 虚拟机4 |                 |      |        |        |



## 六、MyCat管理数据库集群

### 6.1 数据切分

#### 6.1.1 什么是垂直切分？

垂直切分是按照业务对数据表分类，然后把一个数据库拆分成多个独立的数据库



- 垂直切分可以把数据库的并发压力，分散到不同的数据库节点，但是垂直切分并不能减少单表的数据量。
- 不能跨MySQL节点做表连接查询，只能通过接口方式解决
- 跨MySQL节点的事务，需要用分布式事务机制来实现



#### 6.1.2 什么是水平切分？

水平切分是按照某个字段的某种规则，把数据切分到多张数据表



- 水平切分可以把数据切分到多张数据表，可以起到缩表的作用
- 只有数据量很大的表，才需要使用水平切分
- 不同数据表的切分规则并不一致，要根据实际业务来确定
- 集群扩容较为麻烦，需要迁移大量的数据

#### 6.1.3 使用切分的注意事项

添加新的分片，硬件成本和时间成本很大，所以要慎重。可以对分片数据做冷热数据分离，把冷数据移出分片来缩表。详见这门MySQL实战课，https://coding.imooc.com/class/274.html



在项目逐步迭代升级的过程中，先是从单节点演化为水平切分的



### 6.2 安装MyCat

- MyCat是基于Java语言的开源数据库中间件产品，具有跨平台性
- 相较于其他中间件产品，MyCat的切分规则最多，功能最全
- 数据库中间件产品并不会频繁更新升级，MyCat功能非常成熟

**安装JDK镜像**

```shell
docker pull adoptopenjdk/openjdk8
docker tag adoptopenjdk/openjdk8 openjdk8
docker rm adoptopenjdk/openjdk8
```

**创建Java容器，在数据卷放入MyCat**

```shell
docker run -d -it --name mycat1 -v mycat1:/root/server --privileged --net=host openjdk8
```

firewall-cmd --zone=public --add-port=8066/tcp --permanent
firewall-cmd --zone=public --add-port=9066/tcp --permanent

irewall-cmd --reload

### 6.3 配置虚拟帐户

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210916233429082.png" alt="image-20210916233429082" style="zoom:50%;" />

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210916233635786.png" alt="image-20210916233635786" style="zoom:50%;" />

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210916233735420.png" alt="image-20210916233735420" style="zoom:50%;" />



编辑server.xml文件  cd  /var/lib/docker/volumes/mycat1/_data/mycat/conf

```xml
<mycat:server>
  ……  
  <user name="admin">
    <property name="password">abc123</property>
    <property name="schemas">neti</property>
  </user>
</mycat:server>
```



<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210916234552799.png" alt="image-20210916234552799" style="zoom:50%;" />

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210916235144817.png" alt="image-20210916235144817" style="zoom:50%;" />



![image-20210917001500788](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917001500788.png)







<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917001924761.png" alt="image-20210917001924761" style="zoom:50%;" />

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917002001854.png" alt="image-20210917002001854" style="zoom:50%;" />

![image-20210917230254535](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917230254535.png)



![image-20210917232649676](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917232649676.png)

![image-20210917234038864](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917234038864.png)

![image-20210917234313913](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917234313913.png)

创建logs文件夹：

docker exec -it mycat1 bash

cd /root/server

cd mycat

mkdir logs

#### 启动mycat

/var/lib/docker/volumes/mycat1/_data/mycat/bin/startup_nowrap.sh

![image-20210917234753188](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210917234753188.png)

不能为空

![image-20210918000539346](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210918000539346.png)

<img src="C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210918002937572.png" alt="image-20210918002937572" style="zoom:50%;" />

在Mycat中只能用sql语句建表，不能用图形界面：

create table teacher(
id int unsigned primary key,
name varchar(200) not null);

create table student(
id int unsigned primary key,
name varchar(200) not null);



EXPLAIN insert teacher (id,name) VALUES (2,'Jack');

热加载： reload @@config_all;

## zookeeper

![image-20211003205218783](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211003205218783.png)

docker pull zookeeper

docker run -d --name z1 -p 2181:2181 -p 3888:3888 -p 2888:2888 --net=swarm_mysql zookeeper



![image-20211003205901047](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211003205901047.png)

cd  /var/lib/docker/volumes/mycat1/_data/mycat/conf



![image-20211003215124008](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20211003215124008.png)

获取全局主键：SELECT next VALUE for mycatseq_global;