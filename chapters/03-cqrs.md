命令与查询职责分离
===

CQRS
---


Django CQRS
---


![Django CQRS](./images/django-cqrs.png)

 - 当用户、管理员创建或者更新新的对象时，对象将被保存到数据。并且依据我们对HayStack的设定，我们将会即时或定时将数据索引到ElasticSearch中。
 - 当用户搜索时，通过ElasticSearch来进行搜索。

在这个过程中，我们主要依赖于HayStack作为Message Queue来将数据从数据库导入搜索引擎。

MySQL / SQL Server + ElasticSearch
