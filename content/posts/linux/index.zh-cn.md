---
weight: 4
title: "Linux"
date: 2022-03-06T10:27:40+08:00
lastmod: 2022-03-06T12:15:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结了基本的Linux使用."

tags: ["Linux", "Ubuntu", "Shell"]
categories: ["Linux"]

lightgallery: true
---

[Espressif]^(乐鑫) 日常工作依赖于[Linux]^(Ubuntu) 开发环境，在此总常用的操作命令及快捷方式，便于判断知识边界和提高复习效率。

## 系统简介

关于Linux的书籍和文章非常多，不同的应用目的常用的工具和指令是不同的，学习的重点可能会有些许差异，在此总结最通用的基础部分。

Linux 只是一个内核。内核指的是一个提供设备驱动、文件系统、进程管理、网络通信等功能的系统软件，内核并不是一套完整的操作系统，它只是操作系统的核心。一些组织或厂商将 Linux 内核与各种软件和文档包装起来，并提供系统安装界面和系统配置、设定与管理工具，就构成了 Linux 的发行版本。

Linux 的发行版本可以大体分为两类：

* 商业公司维护的发行版本，以著名的 Red Hat 为代表；
* 社区组织维护的发行版本，以 Debian 为代表。

把 Red Hat、Ubuntu、SUSE 等直接说成 Linux 其实是不确切的，它们是 Linux 的发行版本，更确切地说，应该叫作“以Linux为核心的操作系统软件包”。

### Ubuntu

Ubuntu 基于知名的 Debian Linux 发展而来，界面友好，容易上手，对硬件的支持非常全面，是目前最适合做桌面系统的 Linux 发行版本，而且 Ubuntu 的所有发行版本都免费提供。

#### 软件管理

系统默认包管理工具为 **apt**

apt-get命令是Debian Linux发行版中的APT软件包管理工具。所有基于Debian的发行都使用这个包管理系统。deb包可以把一个应用的文件包在一起，大体就如同Windows上的安装文件。
我们常用的Ubuntu就是一个基于Debian的发行，我们使用apt-get命令获取这个列表，以下是我整理的常用命令：

```apt-get
sudo apt-get update  更新源
sudo apt-get install package 安装包
sudo apt-get remove package 删除包
sudo apt-cache search package 搜索软件包
sudo apt-cache show package  获取包的相关信息，如说明、大小、版本等
sudo apt-get install package --reinstall  重新安装包
sudo apt-get -f install  修复安装
sudo apt-get remove package --purge 删除包，包括配置文件等
sudo apt-get build-dep package 安装相关的编译环境
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
sudo apt-cache depends package 了解使用该包依赖那些包
sudo apt-cache rdepends package 查看该包被哪些包依赖
sudo apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get check 检查是否有损坏的依赖

```

apt-key命令用于管理Debian Linux系统中的软件包密钥。每个发布的deb包，都是通过密钥认证的，apt-key用来管理密钥。操作指令：APT密钥操作指令。

```apt-get
apt-key list          #列出已保存在系统中key。
apt-key add keyname   #把下载的key添加到本地trusted数据库中。
apt-key del keyname   #从本地trusted数据库删除key。
apt-key update        #更新本地trusted数据库，删除过期没用的key。

```


#### 配置软件安装源

sources.list系统自带的，源是来Ubuntu的官网！安装包比较慢，所以最好切换成国内的

```sources.list
qitas@ubuntu:~$ cd /etc/apt
qitas@ubuntu:/etc/apt$ sudo cp sources.list sources.list.bak
qitas@ubuntu:/etc/apt$ vim sources.list
```




## 技能补全


### 快捷操作


* clear(完全清除，无法向上翻页查看之前信息)
* ctrl+L（屏幕清除，开启新行，依旧可以向上翻页查看之前信息）
* date 查看系统时间
* cat 正常文件查看
* tac 从最后一行开始显示
* nl 显示是会输出行号
* 可翻页查看(只向后)：more，按q停止
* 可翻页查看(可向前或向后)：less，按q停止

### 文件处理

```
改变所属用户chown（应该首先改）
​ chown user text.txt
改文件权限chmod
​ chmod 770 test.txt
​ chmod u+r test.txt
​ chmod u=rw test.txt
改文件所属组
 chgrp user_grp text.txt
```

### 网络管理



编辑网卡配置文件：sudo vi /etc/network/interfaces
```
auto eth0
iface eth0 inet dhcp
or
auto eth0
iface eth0 inet static
address 192.168.3.90
gateway 192.168.3.1
netmask 255.255.255.0
```

### 显示输出


在使用shell语法时，对于& 1 更准确的说应该是文件描述符 1,而1标识标准输出，stdout。对于2 ，表示标准错误，stderr。
2>&1 的意思就是将标准错误重定向到标准输出。这里标准输出已经重定向到了 /dev/null。那么标准错误也会输出到/dev/null
把/dev/null 可以看作"黑洞". 它等价于一个只写文件. 所有写入它的内容都会永远丢失. 而尝试从它那儿读取内容则什么也读不到，偶尔也可以把 & 在命令的最后加上，表示让程序后台执行。

```ls
ls 2>1 测试一下，不会报没有2文件的错误，但会输出一个空的文件1；
ls xxx 2>1测试，没有xxx这个文件的错误输出到了1中；
ls xxx 2>&1测试，不会生成1这个文件了，不过错误跑到标准输出了；
ls xxx >out.txt 2>&1, 实际上可换成 ls xxx 1>out.txt 2>&1；重定向符号>默认是1,错误和输出都传到out.txt了。
```


### 状态查询


常用系统命令包括 Vmstat、sar、iostat、netstat、free、ps、top等

* 查看活动用户：w
* 查看用户登录日志：last
* 查看用户信息：id
* 查看本机ip: ip a
* 查看路由表：ip route
* 查看所有进程：ps -elf
* 实时查看进程：top

监控CPU状态[sar](https://www.cnblogs.com/liyongsan/p/7459523.html)

{{< admonition tip >}}
:(far fa-bookmark fa-fw): sar对系统每方面进行单独统计，会增加系统开销，不过开销可以评估，对系统的统计结果影响不大。
{{< /admonition >}}

下面是sar命令对某个系统的CPU统计输出：

```sar

[root@webserver ~]# sar -u 3 5

输出解释如下：
%user列显示了用户进程消耗的CPU 时间百分比。
%nice列显示了运行正常进程所消耗的CPU 时间百分比。
%system列显示了系统进程消耗的CPU时间百分比。
%iowait列显示了IO等待所占用的CPU时间百分比
%steal列显示了在内存相对紧张的环境下pagein强制对不同的页面进行的steal操作 。
%idle列显示了CPU处在空闲状态的时间百分比。
```
