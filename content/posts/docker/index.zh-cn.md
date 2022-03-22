---
weight: 4
title: "Docker"
date: 2022-03-09T15:50:40+08:00
lastmod: 2022-03-09T16:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Docker使用."

tags: ["ESP-IDF", "Docker"]
categories: ["Docker"]

lightgallery: true
---


## 简介

[Docker](https://www.docker.com/) 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows操作系统的机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

## 使用

```
docker run -it -v /test:/soft centos /bin/bash
```

* -t：--tty，分配终端
* -i：--interactive,交互式启动
* -d：--detach，后台运行
* -v：--volume,挂在数据卷
* -e, --env list  设置env

这样在容器启动后，容器内会自动创建/soft的目录。通过这种方式，我们可以明确一点，即-v参数中，冒号":"前面的目录是宿主机目录，后面的目录是容器内目录。

```
docker run -it --privileged=true -v /test:/soft centos /bin/bash
```

指定--privileged参数解决“Permission denied”

[runoob教程](https://www.runoob.com/docker/docker-tutorial.html)


## 容器

### ESP-IDF

https://hub.docker.com/r/espressif/idf

```
docker pull espressif/idf
```

```build
sudo docker run --rm --privileged -v $PWD:/project -w /project espressif/idf:release-v4.4 idf.py build
sudo docker run --rm --privileged -v /dev:/dev -v $PWD:/project -w /project espressif/idf:release-v4.4 idf.py fullclean build flash
sudo docker run --rm --privileged -v /dev:/dev -v $PWD:/project -w /project espressif/idf:release-v4.4 idf.py set-target esp32s3 build flash
```
* -w: 指定命令执行时，所在的路径
* --rm：容器停止自动删除容器


```alias
alias esp-idf='docker run --rm --privileged -v /dev:/dev -v $PWD:/project -w /project -it espressif/idf:v4.4 bash -c'
```

执行docker run命令带--rm命令选项，等价于在容器退出后，执行docker rm -v。--rm选项不能与-d同时使用，即只能自动清理foreground容器，不能自动清理detached容器，--rm选项也会清理容器的匿名data volumes。

```
esp-idf "idf.py -p /dev/ttyUSB0 flash"
esp-idf "idf.py -p /dev/ttyUSB0 monitor"
```

### ESP-Update-Server

https://github.com/fito-jaeuklee/ESP32_LOCAL_OTA_SERVER

```
docker run -tid -p 8000:8000 --name fw-server -v $PWD:/firmware sglahn/ota-server
```

```
url -X GET \
  http://localhost:8000/firmware \
    -H 'x-ESP8266-version: 1.0'
```

## 互访

目前的容器间互访基本都是基于网络端口实现。

docker run --link 可以用来链接2个容器，使得源容器（被链接的容器）和接收容器（主动去链接的容器）之间可以互相通信，并且接收容器可以获取源容器的一些数据，如源容器的环境变量。

## K8S

K8S 全称 [Kubernetes](https://www.kubernetes.org.cn/k8s) , 是谷歌开源的容器管理系统，构建在Docker之上，深度整合了Docker，提供资源排程、部署执行、服务发现、扩充缩容等一整套工具。

从架构设计层面，我们关注的可用性，伸缩性都可以结合k8s得到很好的解决，如果你想使用微服务架构，搭配k8s，真的是完美，再从部署运维层面，服务部署，服务监控，应用扩容和故障处理，k8s都提供了很好的解决方案。


具体包括以下几点：

* 服务发现与调度
* 负载均衡
* 服务自愈
* 服务弹性扩容
* 横向扩容
* 存储卷挂载

