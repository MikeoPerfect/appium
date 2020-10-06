## 如何对活动启动进行故障排除


### 能力

> ​		Activity类是Android应用程序的重要组成部分，活动的启动和组合方式是平台应用程序模型的基本组成部分。与通过main()方法启动应用的编程规范不同，Android通过在Activity不同的生命周期调用特定的回调方法来在Activity实例中初始化代码。
> &copy; [Android开发人员文档](https://developer.android.com/guide/components/activities/intro-activities)

​		Appium需要知道程序包和活动名称去正确地初始化被测应用。该信息需要在driver capabilities中提供，并且由以下键组成：

- `appActivity`: 主应用程序活动名称
- `appPackage`: 应用程序包名
- `appWaitActivity`: 要等待或首先启动的应用程序活动名
- `appWaitPackage`:  要等待或首先启动的应用程序包名
- `appWaitDuration`: 等待 `appWaitActivity` 启动的最大时间 (以毫秒为单位，默认为20000)

​		以上这些功能都是可选的。如果你没有明确地设置他们，Appium会从APK清单中读取这些值来尝试自动检测他们。尽管，如果应该在设备（`noReset=true`）上已经安装了受测应用程序，则至少需要设置`appActivity`和`appPackage`选项，因为在这种情况下没有可用的软件包清单。如果你没有明确地设置`appWaitPackage` 和`appWaitActivity` 的值，则他们会被自动设为与`appPackage`/`appActivity`的值一致。有关更多的详细信息，清查阅 [appium-adb](https://github.com/appium/appium-adb/blob/master/lib/tools/android-manifest.js) 包中`packageAndLaunchActivityFromManifest` 方法的实现。


### Appium如何启动活动

​		活动由 [Call activity manager `am`](https://developer.android.com/studio/command-line/adb#am)启动. Appium尝试使用`am start`来启动`appPackage`/`appActivity` 组合，直到`appWaitPackage`/`appWaitActivity`启动或者达到`appWaitDuration` 超时时间。当前聚焦的活动名是通过`adb shell dumpsys window windows` 命令输出 (`mFocusedApp` 或者`mCurrentFocus` 条目)中解析出来的。有关更多详细信息，请查阅[appium-adb](https://github.com/appium/appium-adb/blob/master/lib/tools/apk-utils.js) 包中`startApp`, 和`getFocusedPackageAndActivity`方法的实现。


### 可能的问题和解决方案

#### java.lang.SecurityException: 拒绝权限: 启动意图(Intent)

​		完整的错误描述通常看起来像`'java.lang.SecurityException: Permission Denial: starting Intent { act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER] flg=0x10200000 cmp=com.mypackage/.myactivity.MainActivity launchParam=MultiScreenLaunchParams { mDisplayId=0 mBaseDisplayId=0 mFlags=0 } } from null (pid=11366, uid=2000) not exported from uid 10191`。该错误可能表明，通过`appPackage`/`appActivity`传递（或自动隐式检测到）给Appium的应用程序包名和活动名组合不是正确的，无法启动被测程序。解决方案是与应用程序开发人员检查正确的值，并先执行以下命令来手动测试它们：`adb shell am start -W -n com.myfixedpackage/.myfixedactivity.MainActivity -S -a android.intent.action.MAIN -c android.intent.category.LAUNCHER -f 0x10200000`。如果该命令能手动执行成功并在设备上启动必要的应用程序，那么它也将同样适用于Appium。

#### com.myactivity或 com.myapp.com.myactivity 从未启动

​		此异常通常表明第一个应用活动与`appWaitPackage`/`appWaitActivity设置的(或自动检测)不是同一个包/活动。此类错误通常发生在具有多个活动的应用程序中。为了解决此问题，我们应该与应用程序开发人员确认哪个活动/应用包是在应用程序启动时第一个出现的。当前聚焦的活动名可以用上文提到的命令adb shell dumpsys window windows来进行验证。此外，Appium允许在设置`appWaitActivity` 的值时使用通配符。这在活动名是动态生成或并非一直保持不变的时候尤其有用。例如 `com.mycomany.*` 会匹配任意的 `com.mycomany.foo`或`com.mycomany.bar`

​		如果你仔细检查过活动名称是正确的，但是启动仍然超时，请尝试增大`appWaitDuration` 的值。通常，对于大多数应用程序而言，默认的20秒就足够了。但是，某些比较大的应用可能需要更多的时间才能启动并展示第一个活动。拜托了，请不要创造这样的应用。