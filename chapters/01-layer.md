分层
===

分层[^1]是最常见的架构模式了。在我们的生活中，这也是很常见的一种设计模式。

//TODO 需要一个例子

![Presentation Business Data Layer](./images/pbd.png)

图为表示层、业务逻辑层、数据访问层

MVC
---

下图亦为上中所说的分层结构：

![MVC](./images/mvc.png)


### 项目结构

体现在项目目录结构上的分层，如下是常见的Spring MVC项目的目录结构

 - controller
 - interceptor
 - model
 - service
 - mapper
 - transform

类似的还有，Ruby On Rails的目录结构：

 - assets
 - controllers
 - helpers
 - mailers
 - models
 - views

从这些结构里，我们可以看到xx

当然，也会有一些更有趣的例子，如Python的Django默认的是这样的结构：

```shell
.
├── accounts
│   ├── __init__.py
│   ├── migrations/
│   ├── models.py
│   ├── urls.py
│   └── views.py
└── aggregator
    ├── __init__.py
    ├── admin.py
    ├── management/
    ├── migrations/
    ├── models.py
    └── views.py
```

实践
---

### Spring MVC

[^1]: 让我们致敬Martin Fowler的《企业应用架构模式》
