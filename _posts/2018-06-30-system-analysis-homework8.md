---
title: "System Analysis: Homework 8"
categories:
  - System Analysis and Design
tags:
  - homework
---

## 使用 ECB 实现 make reservation 用例的详细设计（包含用例简介，顺序图，类图）

### 用例简介

* 用户选择要预定的酒店，选择时间、房间等等，再输入姓名、邮箱等信息确认订单。
* 前端发送这些信息给服务器，服务器检查无误后返回给前端通知跳转到付款页面。
* 用户提交付款请求给服务器，服务器通知跳转到第三方系统进行支付，支付成功后返回成功页面给前端。

### 顺序图

![sequence](/assets/images/system_analysis/hw8_sequence.png)

### 类图

![class](/assets/images/system_analysis/hw8_class.png)

## 将逻辑设计类图映射到实际项目框架的包图。用树形结构表述实现的包和类

![tree](/assets/images/system_analysis/hw8_tree.png)
