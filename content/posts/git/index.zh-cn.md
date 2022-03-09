---
weight: 4
title: "Git"
date: 2022-03-08T18:17:40+08:00
lastmod: 2022-03-08T18:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结Git使用."

tags: ["Git", "Github"]
categories: ["tools"]

lightgallery: true
---


## rebase

{{< admonition tip >}}
:(far fa-bookmark fa-fw): 不要通过rebase对任何已经提交到公共仓库中的commit进行修改
{{< /admonition >}}


 ```
 git rebase -i  [startpoint]  [endpoint]
 git rebase -i HEAD~3 
 git rebase -i 36224db
```

* pick：保留该commit（缩写:p）
* reword：保留该commit，但我需要修改该commit的注释（缩写:r）
* edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）
* squash：将该commit和前一个commit合并（缩写:s）
* fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）
* exec：执行shell命令（缩写:x）
* drop：我要丢弃该commit（缩写:d）

将该指定的提交复制到对应分支

 ```
git rebase   [startpoint]   [endpoint]  --onto  [branchName]
```
