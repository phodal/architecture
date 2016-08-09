命令与查询职责分离
===

命令与查询职责分离主要用于那些查询多，而插入少的应用程序，如搜索网站等等。网站客户的数据、网站用户使用的持久化数据中心不是同一个，如我们可以SQL来存储客户的数据，通过消息队列将数据导入搜索引擎中，提供给网站用户使用。

CQRS
---


Django CQRS
---


![Django CQRS](./images/django-cqrs.png)

 - 当用户、管理员创建或者更新新的对象时，对象将被保存到数据。并且依据我们对HayStack的设定，我们将会即时或定时将数据索引到ElasticSearch中。
 - 当用户搜索时，通过ElasticSearch来进行搜索。

在这个过程中，我们主要依赖于HayStack作为Message Queue来将数据从数据库导入搜索引擎。

MySQL / SQL Server + ElasticSearch
