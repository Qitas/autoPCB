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

这样在容器启动后，容器内会自动创建/soft的目录。通过这种方式，我们可以明确一点，即-v参数中，冒号":"前面的目录是宿主机目录，后面的目录是容器内目录。

```
docker run -it --privileged=true -v /test:/soft centos /bin/bash
```

指定--privileged参数，解决“Permission denied”



## ESP-IDF

https://hub.docker.com/r/espressif/idf

```
docker pull espressif/idf
```

```build
docker run --rm --privileged -v $PWD:/project -w /project espressif/idf:v4.4 idf.py build
```


```alias
alias esp-idf='docker run --rm -v $PWD:/project -w /project -it espressif bash -c'
```

```配置与编译
cd ~/myproject/examples/hello-world
esp-idf "idf.py menuconfig"
esp-idf "idf.py build"
```

```alias
alias esp-idf='docker run --rm --privileged -v /dev:/dev -v $PWD:/project -w /project -it espressif/idf:v4.4 bash -c'
```

执行docker run命令带--rm命令选项，等价于在容器退出后，执行docker rm -v。--rm选项不能与-d同时使用，即只能自动清理foreground容器，不能自动清理detached容器，--rm选项也会清理容器的匿名data volumes。

```fash
esp-idf "idf.py -p /dev/ttyUSB0 flash"
esp-idf "idf.py -p /dev/ttyUSB0 monitor"
```