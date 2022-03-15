---
title: docker技巧
date: 2021-04-30 11:06:09
tags:
---

# 1. 安装

## 参考
+ https://blog.csdn.net/Sun_Hui_/article/details/100581161
+ https://docs.docker.com/engine/install/ubuntu/

## local mirrors
1. 编辑文件加入源
```
vim /etc/docker/daemon.json
{
 "registry-mirrors": ["https://obou6wyb.mirror.aliyuncs.com"]
}
```
2. 重启服务
```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

# 2. docker 命令

## 基本命令
+ Search specific image

```
docker search <image_name>
```

+ download a image

```
docker pull <image_name>
```

+ List all image

```
docker image ls
```

或

```
docker images
```

+ List all containers

```
docker ps [-a]
```

+ stop specific container

```
docker stop <container_id>
```

+ remove specific container(needed to be stoped first)

```
docker rm <container_id>
```

+ run container as a daemon

```
docker run -dit <image_name>
```

+ （接上步）连接一个作为daemon运行的container

```
docker exec -it <container_id> /bin/bash
```

## 备份一个容器
+ 参考：https://www.cnblogs.com/boshen-hzb/p/6373549.html
1. 查看当前容器

```
docker ps
```

2. 选择想要备份的容器，然后创建该容器的快照

```
docker commit <container_id> <backup_image_name>
```

如：
```
docker commit 30b8f18f20b4 container-backup
```

3. 查看生成的镜像

```
docker images
```

4. 备份镜像到文件

```
docker save -o <backup_image_name>.tar <backup_image_name>
```

如：
```
docker save -o ~/container-backup.tar container-backup
```

5. 恢复备份镜像

```
docker load -i <backup_image_name>.tar
```

如：
```
docker load -i ~/container-backup.tar
```

6. 查看恢复的镜像

```
docker images
```

7. 使用备份镜像来生成容器

```
docker run -d -p 80:80 container-backup
```

