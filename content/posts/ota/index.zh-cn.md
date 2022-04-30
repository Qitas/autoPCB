---
weight: 4
title: "OTA"
date: 2022-03-27T11:50:40+08:00
lastmod: 2022-03-27T12:05:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结OTA."

tags: ["ota", "espressif"]
categories: ["espressif"]

lightgallery: true
---

[OTA](https://www.espressif.com/zh-hans/products/sdks/esp-idf) (Over-the-Air) 通过无线方式实现固件升级

## ESP OTA

[ESP OTA](https://docs.espressif.com/projects/esp-idf/zh_CN/latest/esp32s3/api-reference/system/ota.html) 基于多分区管理，提供基于WiFi和蓝牙的空中升级方式，特别是通过https连接获取固、完整性校验和回滚机制等整套解决方案，开发者基于 [esp_https_ota](https://github.com/espressif/esp-idf) 组件获得很高的开发起点。
