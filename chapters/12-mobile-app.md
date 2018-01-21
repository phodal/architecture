【架构拾集】：一步步设计一个移动应用架构
===

> 如何 GET 架构设计的新技能

在这一个多月里，我工作在一个采用插件化的原生 Android 应用项目上。随着新技术的引入，及编写原生 Android 代码的技能不断提升，我开始思索如何去解锁移动应用新架构。对，我就是在说 Growth 5.0。

两星期前，我尝试使用了 Kotlin + React Native + Dore + WebView 搭建了一个简单的 Android 移动应用模板。为了尝试解决 Growth 3.0+ 出现的一系列问题：启动速度慢、架构复杂等等的问题。

PS：作为 Architecture 练习计划的一部分，我将采用规范一些的叙述方式来展开。

 1. 业务架构
 2. 技术远景
 3. 方案对比
 4. 架构设计方案
 5. 持续集成方案
 6. 测试策略
 7. 架构实施

业务架构
---

> 技术是为了解决业务的问题而产生的。

脱离了业务，技术就没有了存在的前提。脱离了业务的架构不叫 “架构”，而叫刷流氓，又或者是画大饼。

_Growth_ **提供** _编程学习服务_ **使用** _Web开发路线_ **帮助** _新手 Web 程序员_ **解决** _Web 学习路径问题_。

不过，我还是我喜欢最近对于 Growth 的价值定位：**带你成为顶尖开发者**。

让我们来看一下复杂的说明（30 秒演讲）：

 -          |     - 
------------|-----------
对于        | 缺少 Web 体系经验的程序员
他们有      | 书籍、在线教程、论坛、技术问答、练习项目
我们的产品   | 编程学习软件 Growth
是一个      | 移动应用
它可以      | 涵盖Web开发的流程及技术栈，Web开发的学习路线、成长衡量等各方面。
但他不同于  | segmentfault、知乎
它的优势是  | 拥有完整的 Web 开发流程（知识图谱）、配套完整的电子书、提供练习及学习工具。

在原有的业务架构下，我们拥有 Growth、探索、社区、练习四个核心业务，以及用户中心的功能。

![Growth 业务图](growth-bussiness.png)

技术远景
---

![Growth 远景图](growth-vision.png)

在上一节中，我们介绍的是项目的业务远景。而作为一个技术人员，在一个项目里，我们也已经创建自己的技术远景。一来，我们可以创建出可持续演进的架构；二来，可以满足个人的技能需求。

> 远景，即想象中未来的远大景象。技术远景，即想象中未来的技术方面的远大景象。

以 Growth 为例，我的最基本的技术需求是：提升自身的能力，然后才是一个跨平台的技术设施。

从 Growth 1.0、Growth 2.0 采用的 Ionic，到 Growth 3.0 采用的 React Native，它都优先采用一个跨平台的移动应用开发框架。

 - 跨平台的基本设施
 - React Native 的版权问题
 - 插件化方案
 - 技术实施

考虑到 React Native 本身的不加密，其对于应用来说，存在一些安全的风险。与此同时，使用 React Native

生成的 ``index.android.bundle`` 文件有 3.1M，这个体积相当的大，以至于即使在高通的骁龙 835 处理器上，也需要 4~5 秒的打开时间。

方案对比
---

以下数据，**纯属个人使用体验总结，没有任何的数据基础**：

   -       |   原生   | React Native  | NativeScript  | 混合应用
-----------|----------|--------------|---------------|------------
开发效率    |    2     |    4         |        3      |    5 
跨平台程度  |    0     |    3         |        3      |    4
性能		   |    5     |    4         |   4           |    2
成熟度     |     5     |    4         |   3           |    5 
安全性     |     5     |    3         |   4           |    2 
总计       |    17      |   18        |   17          |  18

NativeScript 在安全性上比 React Native 好一点点的原因是，使用 NativeScript 的人相对少一点，所以技术成本就高一些。毕竟，macOS 和 Android 手机上也是有病毒的。

技术方案
---

在 Growth 3.0 里，我们选择了使用 React Native + WebView 的构建方式，其原因主要是 WebView 的生态圈比较成熟，有相当多的功能已经 WebView

![架构图 1](arche-1.png)

![架构图 2](arche-2.png)

持续集成
---

### 基础设施

Node.js

ADR

Gradle

### 开发工具

Android Studio、Intellij IDEA

库

### 持续集成

Travis CI 

### 发布策略

仍然使用 pgyer.com

测试策略
---

### 原生部分

``Gradle``、

### React Native 部分

``react-test-renderer``、``jest``、``chai``

### 混合应用部分

架构实施
---

### 创建 Fragement

```
class ArcheReactFragment : ReactFragment() {
    override val mainComponentName: String
        get() = "RNArche"

    private var mReactRootView: ReactRootView? = null
    private var mReactInstanceManager: ReactInstanceManager? = null

    @Nullable
    override fun onCreateView(inflater: LayoutInflater?, group: ViewGroup?, savedInstanceState: Bundle?): ReactRootView? {
        mReactRootView = ReactRootView(activity)
        mReactInstanceManager = ReactInstanceManager.builder()
                .setApplication(activity.application)
                .setBundleAssetName("index.android.bundle")
                .setJSMainModulePath("index")
                .addPackage(MainReactPackage())
                .setUseDeveloperSupport(BuildConfig.DEBUG)
                .setInitialLifecycleState(LifecycleState.RESUMED)
                .build()
        mReactRootView!!.startReactApplication(mReactInstanceManager, "RNArche", null)
        return mReactRootView
    }
}
```

### RN 中注册多个 Component

```
AppRegistry.registerComponent('RNArche', () => App);
AppRegistry.registerComponent('RNArche2', () => App2);
```

### 简单的 WebView

```
@SuppressLint("SetJavaScriptEnabled")
@Nullable
override fun onCreateView(inflater: LayoutInflater?, container: ViewGroup?, savedInstanceState: Bundle?): View? {
    val view = inflater?.inflate(R.layout.fragment_webview, container, false)
    mWebView = view?.findViewById(R.id.webview)

    mWebView!!.loadUrl("file:///android_asset/www/index.html")

    val webSettings = mWebView!!.settings
    webSettings.javaScriptEnabled = true
    mWebView!!.webViewClient = WebViewClient()

    return view
}
```
