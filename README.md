### Happy hacking :\)

项目地址：[https://github.com/shaomingquan/catalyst](https://github.com/shaomingquan/catalyst)

1，catalyst是一个dev阶段的http api框架。致力于创建高内聚低耦合的工程，让我们更专注于业务。

2，专注开发阶段程序组织：

* a\) 通过目录结构提供自然的api分组**隔离及继承**特性。
* b\) **模块高内聚**使得结构无痛拆分，让api层的微服务化更容易。
* c\) 自动的加载代码生成。

3，catalyst是个简单的程序组织框架，不会强加runtime特性。如果需要，catalyst也提供了简单的runtime功能，包括：

* a\) 输入校验。它是一种类似`gin binding`的功能，使用代码生成**去掉了缓慢的runtime反射**。
* b\) crud接口快速搭建（实验中）。使得项目的服务端得以快速上线。

> catalyst经过实际项目的检验，目前已有两个线上项目使用。

### content

#### 简介

* [简介](README.md)
* [功能介绍](jian-jie.md)
* [仓库](cang-ku.md)
* [getting start](an-zhuang-yun-xing.md)
* [项目目录说明](mu-lu-jian-jie.md)
* [TODO](todo.md)

#### 功能接入

* [路由](methods.md)
* [中间件](zi-dong-de-lu-you-ming-ming-kong-jian.md)
* [参数验证](can-shu-yan-zheng.md)
* [crud接口 - 创建](curdjie-kou.md)
* [crud接口 - 调用文档](curdjie-kou-diao-yong-wen-dang.md)

#### 原理简介

* [核心原理](yuan-li-jian-jie/he-xin-yuan-li.md)



