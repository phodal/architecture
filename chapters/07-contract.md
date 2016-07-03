契约
===

前后端分离
---

我们在后台使用Spring MVC作为基础架构、Mustache作为模板引擎，和使用JSP作为模板引擎相比没有多大的区别——由Controller去获取对应的Model，再渲染给用户。多数时候搜索引擎都是依据Sitemap来进行索引的，所以我们的后台很容易就可以处理这些请求。同样的当用户访问相应的页面的时候，也返回同样的页面内容。当完成页面渲染的时候，就交由Backbone来处理相应的逻辑了。换句话来说，从这时候它就变成了一个单页面应用。


![Spring Backbone](./images/spring-backbone.png)
