---
title: "Docker部署"
# author: 
tags:
  - Docker
date: '2022-04-16'
ShowToc: true
draft: true
---

记录Docker应用部署流程, 镜像发布/部署

<!--more-->

---

## 前置知识

## 1 Temp

```bash
#安装
sudo curl -sSL [https://get.docker.com](https://get.docker.com/) | sh
#下载 Docker 图形化界面 portainer
sudo docker pull portainer/portainer
#创建 portainer 容器
sudo docker volume create portainer_data
#运行 portainer
sudo docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```


## 2 Temp

## 参考
- [https://shumeipai.nxez.com/2019/05/20/how-to-install-docker-on-your-raspberry-pi.html](https://shumeipai.nxez.com/2019/05/20/how-to-install-docker-on-your-raspberry-pi.html)


拉取Docker镜像创建Docker Container发布Docker镜像容器数据卷DockerFileRun参考

# 拉取Docker镜像

docker pull python:3.8-slim

# 创建Docker Container



# 发布Docker镜像

docker images 查看镜像  
docker pull image-name :tag 默认最新版本  
docker rmi 删除镜像  
docker em 删除容器  
docker run [command] image-name 由镜像新建一个容器  
    --name="Name"   命名  
    -d  后台运行  
    -it 交互方式运行  
    -p host-port:container-port 指定映射端口  
docker ps 列出当前运行的容器  
docker commit -a="dynais" -m"IMFO" CONTAINER_ID NAME:TAG

![image-20220303180008723](file://D:/Workspace/.Typora%20Images%20Hub/image-20220303180008723.png?lastModify=1657534052)

# 容器数据卷

实现容器之间的数据共享

# DockerFile

FROM  
MAINTAINER  
RUN  
ADD  
WORKDIR  
VOLUME  
EXPOSE

docker build -f DOCKERFILE -t NAME:TAG .

docker image tag rhel-httpd:latest registry-host:5000/myadmin/rhel-httpd:latest  
docker image push registry-host:5000/myadmin/rhel-httpd:latest

# Run

docker run -it --rm --name CONTAINER_NAME IMAGE:TAG

# 参考

1.  [https://docs.microsoft.com/zh-cn/visualstudio/docker/tutorials/docker-tutorial?WT.mc_id=vscode_docker_aka_getstartedwithdocker](https://docs.microsoft.com/zh-cn/visualstudio/docker/tutorials/docker-tutorial?WT.mc_id=vscode_docker_aka_getstartedwithdocker)
    
2.  [https://stackoverflow.com/questions/41984399/denied-requested-access-to-the-resource-is-denied-docker](https://stackoverflow.com/questions/41984399/denied-requested-access-to-the-resource-is-denied-docker)
    
3.  [https://docs.docker.com/engine/reference/commandline/push/](https://docs.docker.com/engine/reference/commandline/push/)
    
4.  [https://www.otakusay.com/337.html](https://www.otakusay.com/337.html)
    
5.  [https://www.runoob.com/docker/docker-build-command.html](https://www.runoob.com/docker/docker-build-command.html)


# 去除缓存构建-方法1

root@ubuntu:/dockerfile/df_test1# docker build-t="df_test9" --no-cache.

说明：

       1）构建的时候，加上--no-cache即可；

docker run -it --rm --name cloud_connector dynais/bbb-azure-iot