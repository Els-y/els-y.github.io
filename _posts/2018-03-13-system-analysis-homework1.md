---
title: "System Analysis: Homework 1"
categories:
  - System Analysis and Design
tags:
  - homework
---

# 一、简单题

## 软件工程的定义

- Software engineering is “(1) the application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software, that is, the application of engineering to software,” and “(2) the study of approaches as in (1).” – IEEE Standard 610.12
- 将系统化的、规范的、可度量的方法用于软件的开发、运行和维护的过程，即将工程化应用于软件开发中。

## 阅读经典名著“人月神话”等资料，解释 software crisis、COCOMO 模型。

### software crisis

软件危机是指落后的软件生产方式无法满足迅速增长的计算机软件需求，从而导致开发与维护过程中出现的软件开发成本日益增长、软件开发进度难以控制、用户对“已完成”系统不满意的现象经常发生、软件产品的质量不可靠、软件的可维护程度低、软件开发生产率跟不上硬件的发展和人们需求的增长等问题。

### COCOMO 模型

构造性成本模型，是由巴里·勃姆 (Barry Boehm) 提出的一种软件成本估算方法。这种模型使用一种基本的回归分析公式，使用从项目历史和现状中的某些特征作为参数来进行计算，由三个不断深入和详细的层次组成。第一层，“基本 COCOMO”，适用对软件开发进行快速、早期地对重要的方面进行粗略的成本估计，但因其缺少不同的项目属性（“成本驱动者”）的因素，所以准确性有一定的局限性。“中级 COCOMO”中考虑进了这些成本驱动者。“详细 COCOMO”加入了对不同软件开发阶段影响的考量。

## 软件生命周期。

指软件的产生直到报废的生命周期。周期内有问题定义、可行性分析、总体描述、系统设计、编码、调试和测试、验收与运行、维护升级到废弃等阶段，这种按时间分程的思想方法是软件工程中的一种思想原则，即按部就班、逐步推进，每个阶段都要有定义、工作、审查、形成文档以供交流或备查，以提高软件的质量。 
主要分为6个阶段：1.可行性分析与计划阶段。2.需求分析阶段。3.设计阶段。4.实现阶段。5.测试阶段。6.运行和维护阶段。

## 按照 SWEBok 的 KA 划分，本课程关注哪些 KA 或知识领域？

按照 version3 的 KA 划分，共有：软件需求、软件设计、软件构建、软件测试、软件维护、软件配置管理、软件工程管理、软件工程过程、软件工程模型和方法、软件质量、软件工程专业实践、软件工程经济学、计算基础、数学基础、工程基金会等 15 个知识领域

本课程关注的知识领域为：

* 软件需求
* 软件设计
* 软件构件
* 软件模型和方法。

## 解释 CMMI 的五个级别。例如：Level 1 - Initial：无序，自发生产模式。

- Level 1 - 初始级 (Initial)：软件过程是无序的，有时甚至是混乱的，对过程几乎没有定义，成功取决于个人努力。管理是反应式的。
- Levle 2 - 可重复级 (Repeatable)：建立了基本的项目管理管理过程来跟踪费用、进度和功能特性。制定了必要的过程纪律，能重复早先类似应用项目取得成功的经验。
- Level 3 - 已定义级 (Defined)：已将软件管理和工程两方面的过程文档化、标准化，并综合成该组织的标准软件过程。所有的项目均使用经批准、剪裁的标准软件过程来开发和维护软件，软件产品的生产在整个软件过程是可见的。
- Level 4 - 量化管理级 (Managed)：分析对软件过程和产品质量的详细度量数据，对软件过程和产品都有定量的理解与控制。管理有一个作出结论的客观依据，管理能够在定量的范围内预测性能。
- Level 5 - 优先管理级 (Optimizing)：过程的量化反馈和先进的新思想、新技术促使过程持续不断改进。

## 用自己语言简述 SWEBok 或 CMMI （约200字）

CMMI全称为能力成熟度模型集成，也可称为软件能力成熟度集成模型，是一个过程改进的方法，目的是帮助组织改进他们的绩效，可以通俗的理解为成功企业做好软件的一套习惯、做法、准则的集合，是如何做好软件的最佳实践集合，先进性毋庸置疑。如果企业按照CMMI的要求做，就有可能称为成功的企业。CMMI分为连续式和阶段式两种表述方式，其中阶段式比较容易理解。阶段式分为5个级别，企业通过满足当前级别的所有要求来获得该级别的评级。

# 二、解释 PSP 各项指标及技能要求：

* 阅读《现代软件工程》的 PSP: Personal Software Process 章节。 <http://www.cnblogs.com/xinz/archive/2011/11/27/2265425.html>
* 按表格 PSP 2.1， 了解一个软件工程师在接到一个任务之后要做什么，需要哪些技能，解释你打算如何统计每项数据？ （期末考核，每人按开发阶段提交这个表）

## PSP 各项指标

- Planning：计划
  - Estimate：估计这个任务需要多少时间


- Development：开发
  - Analysis：分析需求
  - Design Spec：生成设计文档
  - Design Review：设计复审（和同事审核设计文档）
  - Coding Standard：代码规范（为目前的开发制定合适的规范）
  - Design：具体设计
  - Coding：具体编码
  - Code Review：代码复审
  - Test：测试（包括自我测试，修改代码，提交修改）
- Record Time Spent：记录时间花费
- Test Report：测试报告
- Size Measurement：计算工作量
- Postmortem：事后总结
- Process Improvement Plan：提出过程改进计划

## 技能要求

- 自我管理的能力
- 团队执行能力
- 时间管理能力
- 对应的编程技术能力

需要对自己的能力有所了解，从而能够预估自己完成任务的时间，同时需要了解软件工程的许多设计模式，从而才能够比较好的设计，然后要有技术能力以及自学能力，至少需要自己应该怎么做，不知道的时候要知道应该可以咨询谁，当编码工作完成后，需要有测试能力，这些都是一些硬实力；同时也是需要许多软实力的，比如说，要有自控能力，要能坚持，要对编码有兴趣等等。

## 统计数据

对每一项数据分开统计，按照每部分所花费的有效时间按小时进行统计。