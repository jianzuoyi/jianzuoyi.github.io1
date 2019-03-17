---
layout: post
title: 【software】docker安装以及常见问题处理方法
tags: 软件
category: 软件
date: 2019-03-16 11:00:00
---

**centos平台安装**

```
# uninstall
sudo service docker stop
sudo yum remove docker-engine

# install
sudo yum install https://get.docker.com/rpm/1.7.1/centos-6/RPMS/x86_64/docker-engine-1.7.1-1.el6.x86_64.rpm

# 非root运行docker：创建docker组，将用户加入docker组
sudo groupadd docker
sudo usermod -aG  docker $USER
# sudo gpasswd -a ${USER} docker
# 查看是否添加成功
cat /etc/group | grep ^docker

# 为docker寻找较大的存储空间
# 1： 停止docker服务
sudo service docker stop
# 2： 移动目录位置
sudo mv /var/lib/docker /path/to/large/disk/docker
# 3： 创建软链接
sudo ln -s /path/to/large/disk/docker /var/lib/docker

# 启动docker服务
sudo service docker start
# 重启docker服务
sudo service docker restart 

# 终端退出登录
exit

重新ssh登录
ssh username@ip
```

**ubuntu平台安装**

```
# unintall
sudo service docker stop
sudo apt-get remove docker docker-ce docker.io

# install
apt-get install docker-ce

# 其他操作见centos平台安装方法

```

**docker的常见使用方法**
```
# 进入docker
docker run -it helloworld:v1.0

# 进入docker的同时挂载外部目录
docker run -it -v /data:/data helloworld:v1.0

# docker run 常用参数
--rm

# 查看镜像
docker images

# 查看运行中的镜像
docker ps -a
```

# Dockerfile例子
```
pass
```
<center>-END-</center>
