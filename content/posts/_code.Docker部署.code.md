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
- 