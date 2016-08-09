读写分离
===

读写分离有一个常见的实践就是页面缓存。我们使用缓存服务器对用户常访问的内容进行缓存，如变成静态文件。这时候它就是一个很简单的读写分离。

页面缓存
---

![HTTP Cache](./images/httpcachemiss.png)

编辑-发布分离
---

编辑-发布分离[^EditingPublishingSeparation]

让我愉快地盗张图：

![编辑-发布分离](./images/edit-pub.png)


[^EditingPublishingSeparation]: 即Editing Publishing Separation，出自于Martin Fowler的相关文章 [EditingPublishingSeparation](http://martinfowler.com/bliki/EditingPublishingSeparation.html)
