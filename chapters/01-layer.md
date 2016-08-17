分层
===

分层[^1]是最常见的架构模式。这种形式的分层在代码中的体现比较明显——我们很容易可以从项目的代码中，毕竟它可以直接体现在项目目录结构上。

如下是常见的Spring MVC项目的目录结构：

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

相似功能的代码以文件夹的形式归纳到一起：

 - 将控制器的相关逻辑放至controllers目录中，由它来对请求进行转发，并进行处理。
 - 将一些请求在进入控制器之前的代码放置interceptor中，由其对用户的那些不需要直接交由controller的请求做特殊做处理。
 - 在model中放置模型相关的代码，如数据的管理、数据库的设计等等。
 - mapper?
 - 将业务逻辑相关的代码放置service目录，由其来对领域知识做一些抽象，而不是交由controller来负责。
 - 我们将一些模型转换为API的操作放置在transform目录中。



![Presentation Business Data Layer](./images/pbd.png)

图为表示层、业务逻辑层、数据访问层

MVC
---

下图亦为上中所说的分层结构：

![MVC](./images/mvc.png)

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

可惜的是，我对Spring MVC已经有些疏远了，在搭建的过程中经常犯一些新手错误。

### Spring MVC

[^1]: 让我们致敬Martin Fowler的《企业应用架构模式》
