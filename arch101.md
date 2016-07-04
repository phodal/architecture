
前言
===
工作两年过去了， 我发现我也学习、实践了一些架构方面的知识。原本我并没有意识到我也可以总结这方面的结识——对于一个刚工作两年的人来说，这有点出乎意料。总结对于自己来说，是一个非常有益的过程。只有当我们总结了自己的知识时，我们才能意识到我们学习到了怎样的知识。

关于架构方面的书籍有相当的多，这只是我对于我所知道并实践过的架构知识的总结。换句话来说，这是我的又一次[RePractise](https://github.com/phodal/repractise)。

作为[Growth](https://github.com/phodal/growth)计划的一部分，这一本电子书的内容会围绕架构以及解决方案两个目标而展开。

分层
===

分层是最常见的架构模式了，除此还有



![Presentation Business Data Layer](./images/pbd.png)

图为表示层、业务逻辑层、数据访问层

MVC
---

![MVC](./images/mvc.png)

实践
---

### Spring MVC

### 项目结构

体现在项目目录结构上的分层

 - controller
 - interceptor
 - model
 - service
 - transform / dao

读写分离
===

页面缓存
---

编辑-发布分离
---

命令与查询职责分离
===



CQRS
---


实践
---

MySQL / SQL Server + ElasticSearch

静态
===

微服务
===

消息队列
===

契约
===

前后端分离
---

我们在后台使用Spring MVC作为基础架构、Mustache作为模板引擎，和使用JSP作为模板引擎相比没有多大的区别——由Controller去获取对应的Model，再渲染给用户。多数时候搜索引擎都是依据Sitemap来进行索引的，所以我们的后台很容易就可以处理这些请求。同样的当用户访问相应的页面的时候，也返回同样的页面内容。当完成页面渲染的时候，就交由Backbone来处理相应的逻辑了。换句话来说，从这时候它就变成了一个单页面应用。


![Spring Backbone](./images/spring-backbone.png)

管道和过滤器
===


Unix管理
---

搜索
---

六边形架构
===


Lan
---

![Lan Server Layer](./images/lan-server.jpg)

![Lan](./images/lan.png)

Clean
===

领域
===


领域特定语言
---

DDD
---
