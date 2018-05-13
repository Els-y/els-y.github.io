---
title: "System Analysis: Homework 6"
categories:
  - System Analysis and Design
tags:
  - homework
---

# 奇妙清单 建模练习

业务文档：[奇妙清单](https://github.com/Baoleme/Dashboard/blob/master/ModelingExercise/%E4%B8%9A%E5%8A%A1%E6%96%87%E6%A1%A3.md)

## 用例图

![usecase](/assets/images/system_analysis/hw6_usecase.png)

## 新建清单及任务的活动图

![activity](/assets/images/system_analysis/hw6_activity.png)

## 清单管理领域模型

![domain](/assets/images/system_analysis/hw6_domain.png)

## 任务的状态图

![state](/assets/images/system_analysis/hw6_task_state.png)

## 新建任务的系统顺序图

![add task](/assets/images/system_analysis/hw6_sequence.png)

## 操作协议

### 契约CO1: 获取清单列表

* 操作：获取清单列表
* 交叉引用：新建任务
* 前置条件：无
* 后置条件：无

### 契约CO2：添加任务

* 操作：添加任务
* 交叉引用：新建任务
* 前置条件：已创建清单
* 后置条件：
  * 创建了任务实例 t
  * t 被关联到清单 l
  * t 的属性被初始化，含有简单描述

### 契约CO3：编辑任务

* 操作：编辑任务
* 交叉引用：新建任务
* 前置条件：正在编辑中的任务
* 后置条件：
  * 任务 t 的详情被修改