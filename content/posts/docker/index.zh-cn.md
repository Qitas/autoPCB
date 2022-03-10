---
weight: 4
title: "Docker"
date: 2022-03-09T11:57:40+08:00
lastmod: 2022-03-09T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Vscode使用."

tags: ["Vscode", "Docker"]
categories: ["Docker"]

lightgallery: true
---


## 简介

[Docker](https://www.docker.com/) 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows操作系统的机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。



## ESP-IDF

https://hub.docker.com/r/espressif/idf

```
docker pull espressif/idf
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
alias esp-idf='docker run --rm --privileged -v /dev:/dev -v $PWD:/project -w /project -it espressif bash -c'
```

```fash
esp-idf "idf.py -p /dev/ttyUSB0 flash"
esp-idf "idf.py -p /dev/ttyUSB0 monitor"
```