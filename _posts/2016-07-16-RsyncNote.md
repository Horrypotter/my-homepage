---
layout: default
title: RsyncNote
---

#应用超市同步笔记


##1. 配置两台服务器的rsync的配置
执行：
vi /etc/rsyncd.conf
写入（括号里的不能写入）：
uid=root
uid=root
gid=root
max connections=36000
use chroot=no
log file=/var/log/rsyncd.log
pid file=/var/run/rsyncd.pid
lock file=/var/run/rsyncd.lock
secrets file=/etc/rsync.pass                 （密码对文件，格式：root:123456   需要创建此文件，并付权限）
[tongbu]                                       （模块名字）
path=/appImage									（同步路径）
comment = server1
ignore errors=yes
read only = no
auth users=root
hosts allow = 10.30.3.83						（同步到某台服务器的ip）
hosts deny = *

注意：password.rsync文件存放位置：/etc/  格式：123456   作用:提供密码进行验证
chmod 600 /etc/password.rsync 必须付权限



##2. 两台服务器分别启动rsync ： rsync --daemon 首次启动（rsync --daemon --config=/etc/rsyncd.conf）

##3. 执行：cd appImage
          rsync -artuz -R ./ 10.30.3.82::tongbu --password-file=/etc/password.rsync（为保持双向同步，不用--delete）
 
 注意：
rsync -artuz -R  --delete ./ 10.30.3.83::tongbu --password-file=/etc/password.rsync
--delete 如果服务器删除了这一个文件，那么客户端也删除，为了保持双向同步，不用此命令
此命令执行完，就对目标服务器同步一次，如果需要定时同步，需要写定时脚本。

双向定时同步（不能同步删除，只能同步增加。因为当a服务器增加了一个文件时，a上的同步脚本将使a服务器和b服务器上的文件对比，将发现a服务器比b服务器多了一个文件，为了同步，将会删除这个文件，这样a服务器无法增加文件）

定时脚本：

#!/bin/bash
cd /appImage
rsync -artuz -R ./ 10.30.3.82::tongbu --password-file=/etc/password.rsync

注意：定时脚本 保存完后 需要执行  chnod 777 tongbu.sh

执行：crontab –e
添加内容：*/1 * * * * /lb/software/tongbu.sh > /dev/null 2>&1