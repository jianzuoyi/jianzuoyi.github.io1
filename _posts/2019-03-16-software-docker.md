---
layout: post
title: 【software】docker安装以及常见问题处理方法
tags: 软件
category:软件
---

### 在centos平台的安装方法
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
# 1： 先停止docker服务
sudo service docker stop
# 2： 移动目录位置
sudo mv docker /path/to/large/disk/docker
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

<center>-END-</center>
