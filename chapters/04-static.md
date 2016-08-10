静态
===

静态是最好的解
---

GitHub Page
---

下图是基于Jekyll的GitHub Page的生成过程[^jekyll]

![静态网站](./images/what-is-a-static-website.png)

静态网站生成
---


编辑-发布-分离
---

如React一样解决DOM性能的问题就是跳过DOM这个坑，要跳过动态网站的性能问题就是让网站变成静态。

越来越多的开发人员开始在使用Github Pages作为他们的博客，这是一个很有意思的转变。主要的原因是这是免费的，并且基本上可以保证24x7小时是可用的——当且仅当Github发现故障的时候才会不可访问。

在这一类静态站点生成器(Github)里面，比较流行的有下面的内容（数据来源： http://segmentfault.com/a/1190000002476681）:

1. Jekyll / OctoPress。Jekyll和OctoPress是最流行的静态博客系统。
2. Hexo。Hexo是NodeJS编写的静态博客系统，其生成速度快，主题数量相对也比较丰富。是OctoPress的优秀替代者。
3. Sculpin。Sculpin是PHP的静态站点系统。Hexo和Octopress专注于博客，而有时候我们的需求不仅仅是博客，而是有类似CMS的页面生成需求。Sculpin是一个泛用途的静态站点生成系统，在支持博客常见的分页、分类tag等同时，也能较好地支持非博客的一般页面生成。
4. Hugo。Hugo是GO语言编写的静态站点系统。其生成速度快，且在较好支持博客和非博客内容的同时提供了比较完备的主题系统。无论是自己写主题还是套用别人的主题都比较顺手。

通常这一类的工具里会有下面的内容：

1. 模板
2. 支持Markdown
3. 元数据

如Hexo这样的框架甚至提供了一键部署的功能。

在我们写了相关的代码之后，随后要做的就是生成HTML。对于个人博客来说，这是一个非常不错的系统，但是对于一些企业级的系统来说，我们的要求就更高了。如下图是Carrot采用的架构：

![Carrot](./images/carrot.png)

这与我们在项目上的系统架构目前相似。作为一个博主，通常来说我们修改博客的主题的频率会比较低， 可能是半年一次。如果你经常修改博客的主题，你博客上的文章一定是相当的少。

上图中的编辑者通过一个名为Contentful CMS来创建他们的内容，接着生成RESTful API。而类似的事情，我们也可以用Wordpress + RESTful 插件来完成。如果做得好，那么我想这个API也可以直接给APP使用。

上图中的开发者需要不断地将修改的主题或者类似的东西PUSH到版本管理系统上，接着会有webhook监测到他们的变化，然后编译出新的静态页面。

最后通过Netlify，他们编译到了一起，然后部署到生产环境。除了Netlify，你也可以编写生成脚本，然后用Bamboo、Go这类的CI工具进行编译。

通常来说，生产环境可以使用CDN，如CloudFront服务。与动态网站相比，静态网站很容易直接部署到CDN，并可以直接从离用户近的本地缓存提供服务。除此，直接使用AWS S3的静态网站托管也是一个非常不错的选择。

重新设计一个基于GitHub的系统如下：

![编辑-发布-分离](./images/travis-edit-publish-code.png)

从我们设计系统的角度来说，我们会在Github上有三个代码库：

1. Content。用于存放编辑器生成的JSON文件，这样我们就可以GET这些资源，并用Backbone / Angular / React 这些前端框架来搭建SPA。
2. Code。开发者在这里存放他们的代码，如主题、静态文件生成器、资源文件等等。
3. Builder。在这里它是运行于Travis CI上的一些脚本文件，用于Clone代码，并执行Code中的脚本。

以及一些额外的服务，当且仅当你有一些额外的功能需求的时候。

1、 Extend Service。当我们需要搜索服务时，我们就需要这样的一些服务。如我正考虑使用Python的whoosh来完成这个功能，这时候我计划用Flask框架，但是只是计划中——因为没有合适的中间件。
2. Editor。相比于前面的那些知识这一步适合更重要，也就是为什么生成的格式是JSON而不是Markdown的原理。对于非程序员来说，要熟练掌握Markdown不是一件容易的事。于是，一个考虑中的方案就是使用 Electron + Node.js来生成API，最后通过GitHub API V3来实现上传。

So，这一个过程是如何进行的。


整个过程的Pipeline如下所示：

1. 编辑使用他们的编辑器来编辑的内容并点击发布，然后这个内容就可以通过GitHub API上传到Content这个Repo里。
2. 这时候需要有一个WebHooks监测到了Content代码库的变化，便运行Builder这个代码库的Travis CI。
3. 这个Builder脚本首先，会设置一些基本的git配置。然后clone Content和Code的代码，接着运行构建命令，生成新的内容。
4. 然后Builder Commit内容，并PUSH内容。


[^jekyll]: 引自http://jekyllbootstrap.com/

