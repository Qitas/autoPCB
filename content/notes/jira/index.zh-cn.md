---
weight: 4
title: "jira"
date: 2022-03-24T11:57:40+08:00
lastmod: 2022-03-24T12:45:40+08:00
draft: false
author: "Qitas"
authorLink: "https://www.qitas.cn"
description: "这篇文章总结jira使用."

tags: ["jira", "espressif"]
categories: ["jira"]

lightgallery: true
---

## 简介

Jira是Atlassian公司出品的一款事务管理软件。无论是“需求”，还是“BUG”，或是“任务”，都是“事务”的一种，所以Jira可以胜任非常多的角色：需求管理、缺陷跟踪、任务管理等等……因为Jira提供了专门的Scrum视图和Kanban视图，所以特别适合敏捷开发团队使用。大型互联网公司如LinkedIn、Facebook、eBay等内部都在使用Jira。



[Project项目](#Project)
[Issue事务](#Issue)
[Field字段](#Field)
[Workflow工作流](#Workflow)
[Screen视图](#Screen)


## Project

在项目管理范畴内可以看作“项目”的，都是Jira中的项目。Project是Issue的容器。在创建项目时，JIRA会要求你指定“KEY”，这个KEY加上数字，就是Issue的唯一ID了。比如新建一个项目，KEY设置为WEB，那么项目下的第一条Issue就是WEB-1，第二条Issue是WEB-2，依此类推。

## Issue

Issue是Jira核心中的核心，它分为以下几种类型：

* Story 故事（即敏捷开发中的“用户故事”）
* Epic 史诗
* Improvement 提升
* New Feature 新特性
* Bug 缺陷
* Task 任务
* Sub-Task 子任务

## Field

一个Story会有属性：名称、详细描述、提交人、提交时间、优先级、状态等等。这些属性就是Field字段。而所谓的Story，也是Type属性为“Story”的Issue而已，把Type属性改成“Epic”，那这个Story就会变成Epic了。


## Workflow

任务会有不同的状态：待办，进行中，已完成；需求也会有不同的状态：刚提交，待评审，暂缓，已拒绝，开发中，已完成，等等。Workflow就是用来定义定义Issue的状态。

Workflow由两部分组成：

* Status 状态
* Transition 转换动作

## Screen

Screen（视图）还会衍生Screen Scheme和Issue Type Screen Scheme两个概念。Screen这个概念就像空气一样，理所当然，可是对于不懂化学的人来说又无法描述。所以这个我们后面再详细介绍。只要知道，我们在新建Issue、编辑Issue、查看Issue详情时，其实是通过“新建视图”、“编辑视图”、“详情视图”完成的就好了。

