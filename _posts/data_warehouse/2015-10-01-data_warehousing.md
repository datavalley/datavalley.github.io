---
layout: post
title: Data Warehousing学习笔记
category: 数据仓库
tags: Data Warehousing
description: 在这个博客里，我使用了bootstrap作为前端框架，另外通过比较选择了一个还算满意的代码高亮方式
---

原文地址：http://www.tutorialspoint.com/dwh/dwh_tutorial.pdf

---

引子：本文是小z在学习[Data Warehousing](http://www.tutorialspoint.com/dwh/dwh_tutorial.pdf)时做的笔记，主要是对原文的翻译。由于刚接触数据仓库，很多概念理解的有偏差，希望大家谅解，如有不当，欢迎大家指出，谢谢。

----

# 1. 概述

"数据仓库"（Data Warehouse）这一术语由Bill Inmon与1991年提出。根据Inmon的定义，数据仓库是面向主题的、集成的、随时间变化而又稳定的数据集合。数据仓库可以辅助数据分析人员做出明智的决策。

操作性数据库每天都会因为事务的发生而随之改变。如果一个商业经理想要分析之前的产品数据或者供应商数据或者消费数据，那么他会因为没有可用的数据而变得抓狂————历史数据已经由于事务的发生而被覆盖了。

数据仓库从多个维度想我们提供通用和整合的数据，同时，数据仓库也会提供Online Analytical Processing (OLAP)工具。这些工具辅助我们在高维空间中对数据进行有效的交互式分析。

关联规则、聚类、分类和预测分析等数据挖掘方法可以集成到OLAP工具中，从而增强交互式知识挖掘。这就是数据仓库变为当前重要的数据分析平台和在线分析处理平台的原因。

## 理解数据仓库

---

+ 数据仓库本身是一个**数据库**，但独立于企业或组织的操作型数据库
+ 数据仓库中的数据不会频繁的更新
+ 数据仓库存储整合的历史数据，有助于企业或组织分析业务
+ 数据仓库辅助经理组织、分析和使用历史数据进行决策
+ 数据仓库有助于多种应用系统的集成

## 为什么数据仓库独立于操作性数据库

---

+ 操作型数据仓库用于常规任务，例如检索某条记录和索引。数据仓库中的查询通常会很复杂。
+ 操作型数据仓库支持多事务的并发处理。并发控制和恢复机制是操作型数据库必需的功能，从而确保数据库鲁棒性和一致性。
+ 操作型数据库的检索支持读和修改操作。而OLAP检索通常只涉及读操作。
+ 操作型数据库通常仅保存当前数据，而数据仓库存储历史数据。

## 数据仓库的特点

----

数据仓库的主要特点是：

+ **面向主题**：数据仓库围绕某个主题而不是公司当前的操作进行组织。这些主题可以是产品、客户、供应商、销售、利润等等。数据仓库并不关心当前的操作，而聚焦于对数据进行建模和分析，用于决策支持
+ **集成**：数据仓库构建于对多种异质数据源（如关系型数据库、文件）进行整合的基础之上。这些集成增强了数据分析的有效性
+ 随着时间变化：数据仓库中存储某个时间段内的数据，从历史的角度提供数据
+ **不变性**：不变性是指数据仓库中的历史数据不会因为新数据的增加而被擦除。数据仓库独立于操作型数据库，因此操作型数据库中频繁的更新不会反馈到数据仓库中

**注意**：数据仓库不需要事务处理、并发控制和恢复，因为在物理上它独立于操作型数据库。

## 数据仓库的应用

---

就像前面讨论的那样，数据仓库辅助经理人组织、分析数据，从而进行更好的决策。数据仓库在以下领域有着广泛的应用：

+ 金融服务
+ 银行服务
+ 消费品
+ 零售部门
+ 制造业

## 数据仓库的类型

--- 

信息处理、分析处理和数据挖掘是数据仓库的三大应用：

+ 信息处理：数据仓库支持数据处理，例如检索、基本的统计分析以及报表等。
+ 分析处理：数据仓库也支持分析处理，数据仓库中的数据可以通过基本的OLAP操作进行分析,例如切片、上卷、下钻和旋转。
+ 数据挖掘：通过发现隐藏的模式和关联，构建分析模型，执行分类和预测，数据仓库也支持知识发现。数据挖掘的结果也可以使用可视化工具进行展示。

| 数据仓库(OLAP)        | 操作型数据库(OLTP)   |
|  - | -  |
| 处理历史信息     | 处理日常信息 |
| OLAP系统被经理、管理者以及分析人员所使用     | OLTP系统被职员、DBA或者数据库专家所使用 |
| 用于分析业务     | 用于运行业务 |
| 关注信息的输出     | 关注数据输入，面向应用 |
| 星型模型，雪花模型      | ER关系模型|
| 存储历史数据     | 存储当前数据 |
| 提供汇总和整合的数据     | 提供原子的、具体的数据 |
| 提供多视图数据     | 提供具体的、关联数据 |
| 数据大小：100G-100TB     | 100MB-100GB |
| 处理历史信息     | 处理日常信息 |
| 灵活性高     | 性能高 |

# 概念

## 什么是Data Warehousing?
 
----

Data Warehousing就构建和使用数据仓库的过程。数据仓库集成了多种异质数据源的数据，其中每一个数据源都支持分析报告、结构化查询或即时查询以及决策支持。Data Warehousing包括数据清洗、数据集成和数据整合等过程。

## 使用数据仓库中的信息

----

一些决策支持技术可以辅助利用数据仓库中的数据。这些技术帮助高管更加快速和高效的利用数据仓库。高管们可以从数据仓库中�收集数据，并加以分析，在此基础上进行决策。数据仓库中获取的信息可以用于以下领域：

+ 调整产品战略：通过比较季度或者年份之间的销售额，对产品进行重定位，并且产品投资组合，实现良好的产品战略调整
+ 顾客分析：通过分析顾客的购买偏好、购买时间以及预算周期，实现顾客分析
+ 操作分析：Data Warehousing也可以辅助进行顾客关系管理和环境校正。数据仓库中的信息也允许分析商业操作。

## 集成异质数据源

----

有两种方法集成异质数据源：

+ 查询驱动的方法
+ 更新驱动的方法

### 查询驱动的方法

查询驱动是集成异质数据源的传统方法，该方法在异质数据源之上构建包装器和集成器（wrappers and integrators），即中介程序（mediators）。

#### 查询驱动方法的过程

1. 当一个查询被提交到某个客户端后，利用元数据字典将该查询转换为适用于该客户端的形式。
2. 将转换形式后的查询发送到本地查询处理器
3. 该客户端返回的结果集成到全局结果集中。

#### 缺点

1. 查询驱动的方法需要复杂的集成和过滤处理
2. 效率低
3. 对于频繁查询，代价高
4. 对于需要聚合的查询代价也很高

### 更新驱动的方法

当前的数据仓库系统更加倾向于更新驱动的方法。在该方法中，异质数据源中的信息首先被集成、存储到仓库中，用于直接查询和分析。

#### 优点

更新驱动的优点

1. 性能高
2. 数据首先在语义层被拷贝、处理、集成、标记、汇总和重构
3. 对于查询处理，不需要针对每个数据源提供接口处理数据

## 数据仓库工具的作用

+ **数据抽取**：从多种异质数据源中收集数据
+ **数据清洗**：发现并校正数据中的错误
+ **数据转换**：将数据从原始格式转换到适用于数据仓库的格式
+ **数据装载**：对数据进行排序、汇总、整合、检验一致性、构建索引和分区
+ **刷新**：更新数据仓库

**注意**：数据清洗和数据转换是改善数据质量和数据挖掘结果的重要步骤

# 术语

本章我们将讨论数据仓库中经常使用的术语。

## 元数据（Metadata）

----

简单来说，元数据就是关于数据的数据，也就是描述数据的数据。例如，一本书的目录就是关于内容的元数据。换句话说，元数据是概括性的数据，可以指导我们找到具体的数据（好恶心的翻译）。

在数据仓库中，我们可以定义元数据为：

+ 元数据是数据仓库的导航数据
+ 元数据定义了数据仓库中的实体
+ 元数据就像一个目录，帮助决策支持系统定位数据仓库的内容

## 元数据库（Metadata Repository）

----

元数据库是数据仓库的一部分，包含以下元数据：

+ 商业元数据：包括数据拥有者信息、业务定义和变化规则
+ 操作元数据：It includes currency of data and data lineage. Currency of data refers to the data being active, archived, or purged. Lineage of data means history of data migrated and transformation applied on it.（不会翻译）
+ 从操作环境到数据仓库的映射数据：这种元数据包括源数据库及其内容、数据抽取、数据分析、清洗、转换规则、数据刷新和清洗规则。
+ 汇总算法：包括纬度算法、粒度数据、聚合和汇总等


## 数据立方体

----

数据立方体帮助分析师从多维度展示数据。我们可以通过维度和事实来定义数据立方体，其中维度是企业保存数据的实体。

### 数据立方体举例

假设公司想要从销售数据仓库中跟踪关于时间、产品、分公司和地理位置的销售记录。我们可以跟踪这些维度的月度销售额，以及跟踪每个分公司的销售记录。每个维度对应一个维度表。例如，“产品”维表拥有产品名称、产品类型和产品分公司等属性。

下图给出了某个公司关于时间（季度）、产品和地理位置的2-D销售数据视图。

![2维销售数据表](http://datavalley.github.io/img/data_warehousing/2d_table.png)

但是在这种2-d表中，我们只能看到关于时间和产品的记录。上表给出了“New Delpi”每个产品在每个季度的销售额。但是如果我们想指导地理位置这一维度的信息，我们就会需要3-d的表。下表展示了在时间、产品和地理位置三个维度上销售额数据：

![3维销售数据表](http://datavalley.github.io/img/data_warehousing/3d_table.png)

上面的3-d表可以使用3-d数据立方体表示：

![3维销售数据表](http://datavalley.github.io/img/data_warehousing/data_cube.png)

## 数据集市

----

数据集市是企业数据的一个子集，而且数据集市对特定的群体非常有用。也就是说，数据集市中的数据只对特定的群体有意义。例如，市场数据集市只包含与产品、顾客和销售相关的数据。数据集市限制与主题之内。

关于数据集市的几点说明：
+ 数据集市通常部署在windows或者unix/linux的廉价服务器上。
+ 数据集市的开发周期相对较短，一般几周。
+ 如果数据集市不是企业范围内的话，长远来看数据集市的生命周期会比较复杂。
+ 数据集市规模较小。
+ 数据集市是部门定制的。
+ 数据集市的数据源是结构化的数据仓库。
+ 数据集市非常灵活。

下图是数据集市的图形化表示：

![数据集市](http://datavalley.github.io/img/data_warehousing/data_mart.png)