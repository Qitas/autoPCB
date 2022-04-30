---
weight: 4
title: "ESP-IDF"
date: 2022-03-25T11:57:40+08:00
lastmod: 2022-03-25T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结ESP-IDF编程开发."

tags: ["esp-idf", "API", "espressif"]
categories: ["espressif"]

lightgallery: true
---


[ESP-IDF](https://www.espressif.com/zh-hans/products/sdks/esp-idf) 是乐鑫官方的物联网开发框架，适用于 ESP32、ESP32-S 和 ESP32-C 系列 SoC。它基于 C/C++ 语言提供了一个自给自足的 SDK，方便用户在这些平台上开发通用应用程序。

相较于传统MCU厂商提供的SDK组件，IDF更接近开源模板，集成丰富的使用案例资源，尤其是广泛吸纳开源资源，是开发趋势的直观呈现，当然这一特性，对于最求底层稳定，上层差异化的应用开发者十分恼火。

## API


### timer

[64-bit hardware timer](https://docs.espressif.com/projects/esp-idf/zh_CN/v4.4.1/esp32s3/api-reference/system/esp_timer.html)

```
#include "esp_timer.h"
#include "esp_timer_impl.h"
```

```
typedef struct {
    esp_timer_cb_t callback;        //!< Function to call when timer expires
    void* arg;                      //!< Argument to pass to the callback
    esp_timer_dispatch_t method;    //!< Call the callback from task or from ISR
    const char* name;               //!< Timer name, used in esp_timer_dump function
    bool skip_unhandled_events;     //!< Skip unhandled events for periodic timers
} esp_timer_create_args_t;
```

调用接口

* esp_err_t esp_timer_init(void)
* esp_err_t esp_timer_create(const esp_timer_create_args_t *create_args, esp_timer_handle_t *out_handle)
* esp_err_t esp_timer_start_once(esp_timer_handle_t timer, uint64_t timeout_us)
* esp_err_t esp_timer_start_periodic(esp_timer_handle_t timer, uint64_t period)
* esp_err_t esp_timer_stop(esp_timer_handle_t timer)
* esp_err_t esp_timer_delete(esp_timer_handle_t timer)

获取状态

* esp_timer_dump(stdout);
* int64_t esp_timer_get_time(void);
* int64_t esp_timer_get_next_alarm(void);
* bool esp_timer_is_active(esp_timer_handle_t timer);
