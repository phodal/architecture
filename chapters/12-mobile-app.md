【架构拾集】：一步步设计一个移动应用架构
===

> 如何 GET 架构设计的新技能

在这一个多月里，我工作在一个采用插件化的原生 Android 应用项目上。随着新技术的引入，及编写原生 Android 代码的技能不断提升，我开始思索如何去解锁移动应用新架构。对，我就是在说 Growth 5.0。

两星期前，我尝试使用了 Kotlin + React Native + Dore + WebView 搭建了一个简单的 Android 移动应用模板。为了尝试解决 Growth 3.0+ 出现的一系列问题：启动速度慢、架构复杂等等的问题。

PS：作为 Architecture 练习计划的一部分，我将采用规范一些的叙述方式来展开。

 - 技术远景
 - 方案对比
 - 架构设计方案
 - 持续集成方案
 - 测试策略

业务架构
---

脱离了业务的架构不叫 “架构”，而叫刷流氓，又或者是画大饼。

对于——

他们有——

我们的产品——

是一个——

它可以——

但他不同于——

它的优势是——

技术远景
---

跨平台

插件化



方案对比
---

   -       |   原生   | Reac Native   | NativeScript  | 混合应用
-----------|----------|--------------|---------------|------------
开发效率    | 
跨平台程度  |
性能		   |
成熟度     | 
安全性     | 

技术方案
---

### 架构图

### 安全性

### 扩展性

持续集成
---

### 基础设施

Node.js

ADR

Gradle

### 开发工具

Android Studio/Intellij IDEA

库


### 持续集成

Travis CI 

### 发布策略

仍然使用 pgyer.com

测试策略
---

### 原生部分

### React Native 部分

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



