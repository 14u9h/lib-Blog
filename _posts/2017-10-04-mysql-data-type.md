---
layout: post
title: MySQL中的数据类型介绍
categories: 数据库
description: MySql数据类型（MySql Data type）
keywords: MySql,MySql数据类型
---


    文本主要参考了官方文档：http://dev.mysql.com/doc/refman/5.7/en/
 
### 1、概述

    要了解一个数据库，我们也必须了解其支持的数据类型。

    MySQL支持所有标准的SQL数据类型，主要分3类:

        数值类型
        字符串类型
        时间日期类型

另一类是几何数据类型，用的不多，也没多介绍。
下面大、小标题后括号内的数组表示其含有的类型个数。
下面所有结论都经过本人使用MySql Workbench编写SQL验证过或来自官网。

 
### 2、数值类型（12）
    
#### 2.1、整数类型（6）

一张图就能解释清楚了：

![图1]({{ site.url }}/img/3058152425.png)
