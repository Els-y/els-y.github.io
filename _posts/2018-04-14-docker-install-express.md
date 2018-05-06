---
title: "Docker 安装并运行 Express 应用 "
categories:
  - Docker
tags:
  - install docker express
---

> 参考文档：《Docker — 从入门到实践》

# 简介

Docker 最初是 dotCloud 公司创始人 Solomon Hykes 在法国期间发起的一个公司内部项目，它是基于 dotCloud 公司多年云服务技术的一次革新，并于 2013 年 3 月以 Apache 2.0 授权协议开源，主要项目代码在 GitHub 上进行维护。Docker 项目后来还加入了 Linux 基金会，并成立推动 开放容器联盟（OCI）。

Docker 自开源后受到广泛的关注和讨论，至今其 GitHub 项目已经超过 4 万 6 千个星标和一万多个 fork。甚至由于 Docker 项目的火爆，在 2013 年底，dotCloud 公司决定改名为 Docker。Docker 最初是在 Ubuntu 12.04 上开发实现的；Red Hat 则从 RHEL 6.5 开始对 Docker 进行支持；Google 也在其 PaaS 产品中广泛应用 Docker。

Docker 使用 Google 公司推出的 Go 语言 进行开发实现，基于 Linux 内核的 cgroup，namespace，以及 AUFS 类的 Union FS 等技术，对进程进行封装隔离，属于 操作系统层面的虚拟化技术。由于隔离的进程独立于宿主和其它的隔离的进程，因此也称其为容器。最初实现是基于 LXC，从 0.7 版本以后开始去除 LXC，转而使用自行开发的 libcontainer，从 1.11 开始，则进一步演进为使用 runC 和 containerd。

Docker 在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极大的简化了容器的创建和维护。使得 Docker 技术比虚拟机技术更为轻便、快捷。

# 安装 Docker

> Ubuntu 16.04 + 上的 Docker CE 默认使用 overlay2 存储层驱动,无需手动配置。

## 使用 APT 安装

添加使用 HTTPS 传输的软件包以及 CA 证书。

```bash
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

添加软件源的 GPG 密钥。

```bash
$ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```

向 source.list 中添加 Docker 软件源

```bash
$ sudo add-apt-repository \
    "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
```

## 安装 Docker CE

更新 apt 软件包缓存，并安装 docker-ce：

```bash
$ sudo apt-get update

$ sudo apt-get install docker-ce
```

## 启动 Docker CE

```
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

## 建立 docker 用户组

默认情况下，docker 命令会使用 Unix socket 与 Docker 引擎通讯。而只有 root 用户和 docker 组的用户才可以访问 Docker 引擎的 Unix socket。出于安全考虑，一般 Linux 系统上不会直接使用 root 用户。因此，更好地做法是将需要使用 docker 的用户加入 docker 用户组。

建立 docker 组：

```bash
$ sudo groupadd docker
```

将当前用户加入 docker 组：

```
$ sudo usermod -aG docker $USER
```

注销并重新登录。

## 添加国内镜像

在 `/etc/docker/daemon.json` 中写入如下内容（如果文件不存在请新建该文件）

```
{
  "registry-mirrors": [
    "https://registry.docker-cn.com"
  ]
}
```

重启服务

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

## 测试 Hello World

```bash
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
9bb5a5d4561a: Pull complete 
Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```

若能输出以上信息，则安装成功。

# 运行 Express 应用

## 创建 Express 项目

```bash
express docker
```

生成基本框架，来测试。

## 创建 Dockerfile

到 `docker` 目录中，创建一个空文件 `Dockerfile`，编辑并保存。

```
# 指定基础镜像 node
FROM node:8.0.0

# 作者信息
MAINTAINER PML

# 将根目录下的文件都 copy 到 container（运行此镜像的容器）文件系统的 app 文件夹下
ADD . /app/

# cd 到 app 文件夹下
WORKDIR /app

# 安装项目依赖包
RUN npm install

# 配置环境变量
ENV HOST 0.0.0.0
ENV PORT 8000

# 容器对外暴露的端口号
EXPOSE 8000

# 容器启动时执行的命令，类似 npm run start
CMD ["npm", "start"]
```

## 创建镜像

到存放 Dockerfile 目录下，运行命令来构建镜像。

```bash
$ docker build -t <your username>/express-hello .
```

## 列出镜像

```bash
$ docker image ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<your username>/express-hello   latest              7ec9b8b0ba31        5 minutes ago       676MB
hello-world         latest              e38bc07ac18e        2 days ago          1.85kB
node                8.0.0               065e283f68bd        10 months ago       667MB
```

可以看到 `<your username>/express-hello`。

## 基于镜像新建容器并启动

```bash
 $ docker run -p 8000:8000 -d <your username>/express-hello
```

参数

* -d: 后台运行镜像容器
* -p: 绑定一个公共端口到私有容器端口

启动后，在浏览器输入 `localhost:8000` 就可以看到如下页面。

![docker-express](/assets/images/system_analysis/docker_express.png)

## 终止容器

查看容器

```bash
$ docker container ls
```

根据查看的结果，可以找到对应容器的 `CONTAINER ID`，用下述命令即可终止容器。

```bash
$ docker container stop <CONTAINER ID>
```

终止状态的容器可以用 `docker container ls -a` 命令看到。

处于终止状态的容器，可以通过 `docker container start` 命令来重新启动。


