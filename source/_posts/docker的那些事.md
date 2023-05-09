---
title: docker的那些事
tags:
  - docker
categories: 工具
abbrlink: 64794
date: 2023-05-09 22:42:36
---

# 安装docker

```
apt update

apt-get install ca-certificates curl gnupg lsb-release

curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get install docker-ce docker-ce-cli containerd.io

systemctl start docker

apt-get -y install apt-transport-https ca-certificates curl software-properties-common

service docker restart

sudo docker version

sudo docker images
```



# 将容器打包成镜像

```
# -a:作者
# -m:提交成镜像时的说明信息
# -p:在commit时，将容器暂停
# -c:使用Dockerfile指令来创建容器

docker commit -a "fuqiang" -m "描述" 容器名 新镜像名：标识 
```



# 创建包含镜像的容器

```
docker run -it --name 新容器名 -p 宿主端口:容器端口 -v 宿主空间位置:容器空间位置 镜像名 /bin/bash

# 第一次要启动容器
docker start 容器名
docker exec -it 容器名 /bin/bash
```



# 其他常用docker命令

```
# 显示在运行的容器
docker ps
# 显示所有容器
docker ps -a
# 搜索镜像
docker search 镜像名
# 拉取镜像
docker pull 镜像名
# 显示当前docker所有镜像
docker images
```

