---
weight: 4
title: "Vscode"
date: 2022-03-05T11:57:40+08:00
lastmod: 2022-03-05T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Vscode使用."

tags: ["Vscode", "editor"]
categories: ["editor"]

lightgallery: true
---


## 简介

VSCode（Visual Studio Code）是一款由微软开发且跨平台的免费源代码编辑器。该软件支持语法高亮、代码自动补全（又称 IntelliSense）、代码重构、查看定义功能，并且内置了命令行工具和 Git 版本控制系统。用户可以更改主题和键盘快捷方式实现个性化设置，也可以通过内置的扩展程序商店安装扩展以拓展软件功能。

VS Code 使用 Monaco Editor 作为其底层的代码编辑器。和 GitHub 的 Atom一样，Visual Studio Code 也基于 Electron 框架构建。

VScode官网：https://code.visualstudio.com

## 功能

### 快捷方式

* 折叠所有区域代码的快捷： ctrl + k  ctrl + 0 ; 先按下 ctrl 和 K，再按下 ctrl 和 0;
* 展开所有折叠区域代码的快捷：ctrl +k ctrl + J ; 先按下 ctrl 和 K，再按下 ctrl 和 J;


## code-server


[github](https://github.com/coder/code-server)


```Docker
# This will start a code-server container and expose it at http://127.0.0.1:8080.
# It will also mount your current directory into the container as `/home/coder/project`
# and forward your UID/GID so that all file system operations occur as your user outside
# the container.
#
# Your $HOME/.config is mounted at $HOME/.config within the container to ensure you can
# easily access/modify your code-server config in $HOME/.config/code-server/config.json
# outside the container.
mkdir -p ~/.config
docker run -it --name code-server -p 127.0.0.1:8080:8080 \
  -v "$HOME/.config:/home/coder/.config" \
  -v "$PWD:/home/coder/project" \
  -u "$(id -u):$(id -g)" \
  -e PASSWORD='登录密码' \
  -e "DOCKER_USER=$USER" \
  codercom/code-server:latest
```

code-server目前还不支持在线安装插件，不过它提供了.VSIX方式的安装

```
wget https://github.com/Microsoft/vscode-python/releases/download/2019.3.6558/ms-python-release.vsix
```

```Docker
docker run -itd --name coder-idf -p 172.16.0.6:8266:8080 \
  -v "/home/code:/home/code" \
  -u "$(id -u):$(id -g)" \
  -e PASSWORD='12345678' \
  -e "DOCKER_USER=$USER" \
  --restart=always \
  codercom/code-server:latest
```


```Docker
sudo docker run -itd --name esp-idf-master -p 192.168.171.41:8266:8080 \
  -v "$HOME/.config:/home/coder/.config" \
  -v "$PWD:/home/coder/esp-idf" \
  -u "$(id -u):$(id -g)" \
  -e PASSWORD='12345678' \
  -e "DOCKER_USER=$USER" \
  --restart=always \
  codercom/code-server:latest
```

