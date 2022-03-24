---
weight: 4
title: "Espressif"
date: 2022-03-05T11:57:40+08:00
lastmod: 2022-03-05T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Espressif编程开发."

tags: ["ESP-IDF", "espressif"]
categories: ["espressif"]

lightgallery: true
---

## esptool

[esptool](https://github.com/espressif/esptool) 是乐鑫提供的开源库工具，用于乐鑫芯片和 ROM Bootloader（一级 bootloader）通讯，从而实现：固件烧录，flash 擦除，flash 读取，读 MAC 地址，读 flash id ，elf 文件转 bin 等常用功能；flash 校验, 读取内存，载入 bin 到 RAM 执行，读内存，写内存，读 flash 状态，写 flash 状态，读 chip id，组装 bin等高级功能。


```
esptool.py read_mac
esptool.py flash_id
```
通常设备有多个 MAC 地址，例如做 station 的 MAC 地址，做 softAP 时的 MAC 地址，这里读取的是 MAC 地址是 station 地址

自动读取从 0x0 地址开始的 4KB 内容，保存到 dump.bin 文件

```
esptool.py read_flash 0x0 0x1000 dump.bin
esptool.py erase_region 0x20000 0x4000
```


## IDF

[ESP-IDF](https://www.espressif.com/zh-hans/products/sdks/esp-idf) 是乐鑫官方的物联网开发框架，适用于 ESP32、ESP32-S 和 ESP32-C 系列 SoC。它基于 C/C++ 语言提供了一个自给自足的 SDK，方便用户在这些平台上开发通用应用程序。


### Docker-IDF

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


## ADF

[ESP-ADF](https://github.com/espressif/esp-adf)
