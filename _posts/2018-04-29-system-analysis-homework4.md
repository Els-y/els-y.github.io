---
title: "System Analysis: Homework 4"
categories:
  - System Analysis and Design
tags:
  - homework
---

# 领域建模

### a. 阅读 Asg_RH 文档，**按用例**构建领域模型。

- 按 Task2 要求，请使用工具 UMLet，截图格式务必是 png 并控制尺寸
- 说明：请不要受 PCMEF 层次结构影响。你需要识别实体（E）和 中介实体（M，也称状态实体）
  - 在单页面应用（如 vue）中，E 一般与数据库构建有关， M 一般与 [store 模式](https://cn.vuejs.org/v2/guide/state-management.html) 有关
  - 在 java web 应用中，E 一般与数据库构建有关， M 一般与 session 有关

![asg](/assets/images/system_analysis/hw4_asg.png)

### b. 数据库建模(E-R 模型)

* 按 Task 3 要求，给出系统的 E-R 模型（数据逻辑模型）

* 建模工具 PowerDesigner（简称PD） 或开源工具 [OpenSystemArchitect](http://www.codebydesign.com/)

* 不负责的链接 <http://www.cnblogs.com/mcgrady/archive/2013/05/25/3098588.html>

  ![](/assets/images/system_analysis/hw4_er.png)

* 导出 Mysql 物理数据库的脚本

  ```sql
  /*==============================================================*/
  /* DBMS name:      MySQL 5.0                                    */
  /* Created on:     2018/4/29 21:49:26                           */
  /*==============================================================*/


  drop table if exists CreditCard;

  drop table if exists Date;

  drop table if exists Hotel;

  drop table if exists Location;

  drop table if exists Reservation;

  drop table if exists Room;

  drop table if exists RoomOrder;

  /*==============================================================*/
  /* Table: CreditCard                                            */
  /*==============================================================*/
  create table CreditCard
  (
     card_id              int not null,
     card_number          varchar(1),
     security_code        varchar(1),
     primary key (card_id)
  );

  /*==============================================================*/
  /* Table: Date                                                  */
  /*==============================================================*/
  create table Date
  (
     date_id              int not null,
     year                 int,
     month                int,
     day                  int,
     primary key (date_id)
  );

  /*==============================================================*/
  /* Table: Hotel                                                 */
  /*==============================================================*/
  create table Hotel
  (
     hotel_id             int not null,
     location_id          int,
     name                 varchar(1),
     location             varchar(1),
     primary key (hotel_id)
  );

  /*==============================================================*/
  /* Table: Location                                              */
  /*==============================================================*/
  create table Location
  (
     location_id          int not null,
     country              varchar(1),
     city                 varchar(1),
     block                varchar(1),
     primary key (location_id)
  );

  /*==============================================================*/
  /* Table: Reservation                                           */
  /*==============================================================*/
  create table Reservation
  (
     reservation_id       int not null,
     hotel_id             int,
     room_order_id        int,
     card_id              int,
     customer_name        varchar(1),
     customer_email       varchar(1),
     requirement          varchar(1),
     smoking              bool,
     total_price          float,
     primary key (reservation_id)
  );

  /*==============================================================*/
  /* Table: Room                                                  */
  /*==============================================================*/
  create table Room
  (
     room_id              int not null,
     hotel_id             int,
     room_number          int,
     type                 int,
     primary key (room_id)
  );

  /*==============================================================*/
  /* Table: RoomOrder                                             */
  /*==============================================================*/
  create table RoomOrder
  (
     room_order_id        int not null,
     room_id              int,
     num_of_people        int,
     check_in             int,
     check_out            int,
     primary key (room_order_id)
  );

  alter table Hotel add constraint FK_Reference_1 foreign key (location_id)
        references Location (location_id) on delete restrict on update restrict;

  alter table Reservation add constraint FK_Reference_10 foreign key (card_id)
        references CreditCard (card_id) on delete restrict on update restrict;

  alter table Reservation add constraint FK_Reference_3 foreign key (hotel_id)
        references Hotel (hotel_id) on delete restrict on update restrict;

  alter table Reservation add constraint FK_Reference_4 foreign key (room_order_id)
        references RoomOrder (room_order_id) on delete restrict on update restrict;

  alter table Room add constraint FK_Reference_2 foreign key (hotel_id)
        references Hotel (hotel_id) on delete restrict on update restrict;

  alter table RoomOrder add constraint FK_Reference_5 foreign key (room_id)
        references Room (room_id) on delete restrict on update restrict;

  alter table RoomOrder add constraint FK_Reference_8 foreign key (check_in)
        references Date (date_id) on delete restrict on update restrict;

  alter table RoomOrder add constraint FK_Reference_9 foreign key (check_out)
        references Date (date_id) on delete restrict on update restrict;
  ```


* 简单叙说 数据库逻辑模型 与 领域模型 的异同
  * 相同点：
    * 都是对实际问题的抽象，表示对象以及它们之间的关系，用于更直观的显示需求。
  * 不同点：
    * 数据库逻辑模型专注于数据库表，更加具体，有属性的类型、主键等约束信息；领域模型专注于功能业务流程，更专注整体性。
    * 领域模型是一个商业建模范畴的概念，他和软件开发没有关系，是用来表述某一领域的业务模型；而数据库逻辑模型是一个软件开发领域的概念，虽然能在一定程度上表示业务体系，但是主要是为了表述数据库中的结构。