---
weight: 4
title: "Camera"
date: 2022-03-06T18:17:40+08:00
lastmod: 2022-03-06T18:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Camera相关知识."

tags: ["Camera", "DVP", "USB"]
categories: ["IoT"]

lightgallery: true
---


## 简介

sensor（图像传感器）是一种半导体芯片，有两种类型：电荷耦合器件CCD（Charge Coupled Device） 和 互补金属氧化物半导体CMOS（Complementary Metal-Oxide Semiconductor）。

* CCD传感器，电荷信号先传送，后放大，再A/D，成像质量灵敏度高、分辨率好、噪声小；处理速度慢；造价高，工艺复杂。
* CMOS传感器，电荷信号先放大，后A/D，再传送；成像质量灵敏度低、噪声明显；处理速度快；造价低，工艺简单。

{{< admonition tip >}}
:(far fa-bookmark fa-fw): ISP（图像信号处理） 主要完成数字图像的处理工作，把 sensor 采集到的原始数据转换为对应格式。
{{< /admonition >}}

### OV2640

支持：RGB565或JPEG输出

UKCA,即分辦率位1600*1200的输出格式。类似的还有：SXGA(1280*1024)、XVGA(1280*960)、WXGA(1280*800)、XGA(1024*768)、SVGA(800*600)、VGA(640ド480)、CIF(352*288)和 QQVGA(160*120)等。

PCLK,即像素时钟,一个PCLK时钟,输出一个(或半个)像素。VSYNC,即帧同步信号。HREF/ HSYNC,即行同步信号。


## interface

* USB（Universal Serial Bus）串行通用串行总线
* MIPI是移动行业处理器接口（Mobile Industry Processor Interface）
* DVP是数字视频端口（digital video port）的简称
* CSI是相机串行接口（CMOS Sensor Interface）的简称

### DVP

DVP总线PCLK极限约在96M左右，而且走线长度不能过长，所有DVP最大速率最好控制在72M以下，PCB layout较容易画；MIPI总线速率lvds接口耦合，走线必须差分等长，并且需要保护，故对PCB走线以及阻抗控制要求高一点（一般来讲差分阻抗要求在85欧姆~125欧姆之间）。

DVP是并口，需要PCLK、VSYNC、HSYNC、D[0：11]——可以是8/10/12bit数据，看ISP或baseband是否支持；

MIPI是LVDS（Low Voltage Differential Signaling，低电压差分信号），低压差分串口。只需要要CLKP/N、DATAP/N——最大支持4-lane，一般2-lane可以搞定。

MIPI接口比DVP的接口信号线少，由于是低压差分信号，产生的干扰小，抗干扰能力也强。

最重要的是DVP接口在信号完整性方面受限制，速率也受限制。500W还可以勉强用DVP，800W及以上都采用MIPI接口。

### MIPI

MIPI是差分串口传输，速度快，抗干扰。主流手机模组现在都是用MIPI传输，传输时使用4对差分信号传输图像数据和一对差分时钟信号；最初是为了减少LCD屏和主控芯片之间连线的数量而设计的，后来发展到高速了，支持高分辨率的显示屏，现在基本上都是MIPI接口。

### CSI

CSI-2接口规范是由MIPI(Mobile Industry Processor Interface)联盟组织于2005年发布的关于相机串行接口，它作为一种全新的相机设备和处理器之间的接口框架，给便携式、手机摄像头等相关产业提供了一种灵活且高速的设备接口。
