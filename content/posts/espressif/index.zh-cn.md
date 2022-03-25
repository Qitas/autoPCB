---
weight: 4
title: "Espressif"
date: 2022-03-15T11:57:40+08:00
lastmod: 2022-03-15T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Espressif编程开发."

tags: ["tools", "espressif"]
categories: ["espressif"]

lightgallery: true
---

## 编程规范

* 1、任何只在单个源文件中使用的变量或函数都应该被声明为静态的（static）
    * 1.1 静态变量应该以s_为前缀，以便于识别
* 2、公共名称（非静态变量和函数）应该用每个组件或每个单元的前缀来命名，以避免命名冲突
* 3.非必要避不用缩写（即把data缩短为dat）
* 4.每个缩进级别使用4个空格，不要使用制表符来缩进
* 5.函数之间空行隔开，函数｛｝中不要以空行开始或结束
* 6.只要不严重影响可读性，最大行长为120个字符
* 7.始终在if、switch、for等条件和循环关键词后面添加个空格，而不是直接加()
    * 7.1 在二进制运算符周围添加单个空格
    * 7.2 单数运算符不需要空格
    * 7.3 乘法和除法运算符周围可以去掉空格v
* 8 有时在一行中添加空格使代码垂直对齐，使代码更易读
    * 8.1 要少用水平对齐，特别是当你预计以后会有新的行被添加到列表中时
* 9 不要在行末添加尾部的空白
* 10 如果暂时禁用某些调用，并打算在将来恢复它，请在相邻行加注释
    * 10.1 对于#if 0 #endif块。如果不使用就完全删除它。否则，添加注释，解释为什么该块被禁用
    * 10.2 不要添加修改日期之类的琐碎的注释，因为这些信息都是可以通过git查出的
* 11 提交的文件应该只包含LF（Unix风格）结尾的文件

```
// IDF Master在使用时会遇到LF/CRLF问题，相关解决方式
git rebase --exec 'git diff-tree --no-commit-id --name-only -r HEAD | xargs dos2unix
&& git commit -a --amend --no-edit --allow-empty' master

//针对单个文件的转码可使用 dos2unix FILENAME

```
* 12 如果不是重构或新加一个文件，不要去改变文件格式，这样便于review修改部分
* 13 配置ESP-IDF可禁用断言assert()，在默认配置中，返回false或0的assert条件将调用abort()并触发一个Fatal Error
* 14 共用头文件需要预处理保护机制，如 #pragma once / #ifndef FILE_NAME_H ... #endif
* 15 共用头文件需要加入 extern "C" 实现和C++代码的兼容
* 16 在#include其他文件时，尽量保持如下顺序
```
//对C语言标准库头文件和其他POSIX头文件使用角括号，格式如 #include <stdio.h>
* C standard library headers.
* Other POSIX standard headers and common extensions to them (such as sys/queue.h.)
* Common IDF headers (esp_log.h, esp_system.h, esp_timer.h, esp_sleep.h, etc.)
* Headers of other components, such as FreeRTOS.
* Public headers of the current component.
* Private headers.

```



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

```
esptool.py --chip esp32c3 merge_bin -o test_flash_c3.bin --flash_mode dio --flash_freq 80m --flash_size 2MB 0x0 build/bootloader/bootloader.bin 0x8000 build/partition_table/partition-table.bin 0x10000 build/uart_test.bin
```

精简后：

```
esptool.py --chip esp32c3 merge_bin -o test_flash_c3.bin 0x0 build/bootloader/bootloader.bin 0x8000 build/partition_table/partition-table.bin 0x10000 build/uart_test.bin
```



## ADF

[ESP-ADF](https://github.com/espressif/esp-adf)
