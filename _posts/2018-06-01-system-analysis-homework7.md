---
title: "System Analysis: Homework 7"
categories:
  - System Analysis and Design
tags:
  - homework
---

## 描述软件架构与框架之间的区别与联系

### 区别

* 架构不是软件，是一个系统的草图，是关于软件如何设计的重要决策，是把系统分解为一些部件，描述这些部件的职责及它们之间的协作行为。软件架构并不仅仅关注软件本身的结构和行为，还注重其他特性：使用、功能性、性能、弹性、重用、可理解、经济以及技术的限制和权衡等。

* 框架是特定语言和技术的架构应用解决方案，算是一种特殊的软件。​软件框架是面向领域（如ERP、计算领域等）的、可复用的“半成品”软件，它实现了该领域的共性部分，并提供了一些定义良好的可变点以保证灵活性和可扩展性。也就是说软件框架是领域分析结果的软件化，是领域内最终应用的模板。

### 联系

* 软件架构是引导如何设计软件框架的重要决策。它决定了软件系统如何划分，在一定程度上描述了被划分的各个部分之间的静态、动态关系。软件架构的决策体现在软件系统的框架中。
* 框架是一个可实例化的、部分完成的软件系统或子系统，它为一组系统或子系统定义了架构，并提供了构造系统的基本构造块，还为实现特定功能定义了可调整点。在面向对象环境中，框架由抽象类和具体类组成。
* 软件架构指导软件框架的设计，而软件框架是一种或多种架构的组合的实现。

## 以你的项目为案例

* 绘制三层架构模型图，细致到分区

![mvc](/assets/images/system_analysis/hw7_mvc.png)

* 结合你程序的结构，从程序员角度说明三层架构给开发者带来的便利
  * 项目结构清晰，有利于明确分工及后期的维护和升级；
  * 耦合度低，可维护性高，可以很容易用新的实现替换原有层次的实现；
  * 开发人员可以只关注整个结构中的某一层，而无需过多关注其它层的实现；
  * 扩展性强，不同层职责不同；
  * 安全性高，视图层无法直接访问数据层，减少了入口点，能够屏蔽高危操作。

## 研究 VUE 与 Flux 状态管理的异同

### Flux 基本概念

Flux 将一个应用分成四个部分。

* View：视图层
* Action（动作）: 视图层发出的消息（比如mouseClick）
* Dispatcher（派发器）：用来接收Actions、执行回调函数
* Store（数据层）：用来存放应用的状态，一旦发生变动，就提醒Views要更新页面

![flux](/assets/images/system_analysis/hw7_flux.png)

Flux 的最大特点，就是数据的"单向流动"。

1. 用户访问 View
2. View 发出用户的 Action
3. Dispatcher 收到 Action，要求 Store 进行相应的更新
4. Store 更新后，发出一个"change"事件
5. View 收到"change"事件后，更新页面

上面过程中，数据总是"单向流动"，任何相邻的部分都不会发生数据的"双向流动"。这保证了流程的清晰。

### Vuex 基本概念

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

Vuex 把组件的共享状态抽取出来，以一个全局单例模式管理。在这种模式下，组件树构成了一个巨大的“视图”，不管在树的哪个位置，任何组件都能获取状态或者触发行为。

![vuex](/assets/images/system_analysis/hw7_vuex.png)

### 异

* 应用组成不同。
* 对数据流的管理方式不同。
  * Flux
    > View 发起 Action --> Action 传递到 Dispatcher --> Dispatcher 接收 Action，并通知 Store 进行更新 --> Store 更新状态并通知 View 进行改变 --> View 收到通知后，更新相应页面内容

    此过程，同步 / 异步操作都相同。
  * Vuex: 没有使用 Dispatcher 来接收 Actions 、执行回调函数并通知 Store 改变状态，而是通过使用 Mutation 来改变状态。状态管理的核心概念如下,
    
    同步操作
    > View 中触发 mutation --> 在 mutation 函数中改变 state --> 通过 getter/setter 实现的双向绑定会自动更新对应的 View
    
    异步操作
    > 在 View 中触发 action，并根据实际情况传入需要的参数 --> 在 action 中触发所需的 mutation，在 mutation 函数中改变 state --> 通过 getter/setter 实现的双向绑定会自动更新对应的 View。

### 同

* Flux 思想是为了解决传统 MVC 架构不能有效解决大型业务中复杂数据流的管理问题而产生的一种软件架构思想。Vuex 和 Flux 的状态管理都是基于 Flux 思想的有效实现，通过对数据流进行严格管理来规范数据在 Web 应用中的流动方式。
* 两者都使用单向数据流进行状态管理。