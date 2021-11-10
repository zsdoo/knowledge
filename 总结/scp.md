```bash

109.67
cd /data/energy/Wechat
scp -prv 2020-12-1[5-9] 2020-12-2[0-9]  2021-01-* ht@172.29.106.5:/data/bak/

106.5
cd /data/bak/temp
scp -P 10090 -prv /data/bak/* ht@124.70.94.30:/data/bak

10.46.5.20
cd /data/energy/Wechat/
mkdir temp
chown ht:ht temp
chown 777 temp

10.46.5.5
cd /data/bak/temp
scp -prv * ht@10.46.5.20:/data/toweralipay/data


scp -P 50022 -prv ht@10.46.5.20:/root/bak.tar.zip /data/


获取充电文件
ftp -n <<EOF
open 180.153.49.212 50022
use billing 1234QWer,
binary
cd /data/charging/
lcd /data/charging/
prompt
mget -c *.csv
quit
EOF

上传文件：(需要新创建文件夹)
ftp -v -n <<EOF
open 180.153.49.212 50022
use billing 1234QWer,
binary
cd /data/energy/Alipay/
mkdir 20210129
cd 20210129
lcd /data/energyalipay/data/20210129
prompt
mput *
quit
EOF
```





![image-20210104131755517](C:\Users\86132\AppData\Roaming\Typora\typora-user-images\image-20210104131755517.png)