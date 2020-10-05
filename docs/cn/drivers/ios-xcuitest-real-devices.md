## Appium XCUITest Driver 真机设置

### 安装依赖

从 1.15.0 版本开始，Appium 通过 [appium-ios-device](https://github.com/appium/appium-ios-device) 和真机交互。
已经不需要安装额外的依赖。

XCUITest driver 会在设备上安装一个名为 `WebDriverAgent-Runner` 的辅助应用，然后通过它操纵待测应用。
虽然理论上简单，但处理签名和 provisioning 让开发和测试变得有点儿麻烦。

Xcode 需要能访问这个设备。请通过 _设备 或 _模拟器 的 Xcode 日志确保测试用的设备可以正常连接到 Xcode。
[appium-xcuitest-driver](https://github.com/appium/appium-xcuitest-driver) 的文档也有助于处理依赖。

### 基础 (自动) 配置

在 iOS 真机上支持 Appium XCUITest 运行的最简单的方法是使用自动配置策略。有两种做法：

*   使用 `xcodeOrgId` 和 `xcodeSigningId` desired capabilities:
```json
    {
      "xcodeOrgId": "<Team ID>",
      "xcodeSigningId": "iPhone Developer"
    }
```
*   新建一个 `.xcconfig` 文件，添加如下内容：
```
    DEVELOPMENT_TEAM = <Team ID>
    CODE_SIGN_IDENTITY = iPhone Developer
```
不论哪种做法，Team ID 是苹果生成后分配给你团队的一个唯一的 10 位字符串。用开发者账号可以找到你的 Team ID。
登录 [developer.apple.com/account](http://developer.apple.com/account)，在边栏点击 Membership。
你的 Team ID 在 Membership Information 分节的 team name 下面。在“钥匙串访问”，你的 iPhone Developer
证书的“组织单位”的值也是 Team ID。

注意这两个做法互斥，使用 `xcodeConfigFile` capability 或者 `xcodeOrgId` 和 `xcodeSigningId`
组合的其中一个。

配置完成后，应该只需要给 `udid` desired capability 指定一个真机就可以开始测试了。

如果没有正常运行，通常会在 Appium server 日志中列出一些错误和`info XCUITest xcodebuild exited with code '65' and signal 'null'`。这通常是因为没有正确设置代码签名。接着可以通过 [基础 (手动) 配置](#basic-manual-configuration) 来修正。

如果真机上成功安装了 `WebDriverAgentRunner`，但是 Appium 日志有这样的错误信息：
```
2017-01-24 09:02:18.358 xcodebuild[30385:339674] Error Domain=com.apple.platform.iphoneos Code=-12 "Unable to launch com.apple.test.WebDriverAgentRunner-Runner" UserInfo={NSLocalizedDescription=Unable to launch com.apple.test.WebDriverAgentRunner-Runner, NSUnderlyingError=0x7fa839cadc60 {Error Domain=DTXMessage Code=1 "(null)" UserInfo={DTXExceptionKey=The operation couldn’t be completed. Unable to launch com.apple.test.WebDriverAgentRunner-Runner because it has an invalid code signature, inadequate entitlements or its profile has not been explicitly trusted by the user. : Failed to launch process with bundle identifier 'com.apple.test.WebDriverAgentRunner-Runner'}}}
2017-01-24 09:02:18.358 xcodebuild[30385:339674] Error Domain=IDETestOperationsObserverErrorDomain Code=5 "Early unexpected exit, operation never finished bootstrapping - no restart will be attempted" UserInfo={NSLocalizedDescription=Early unexpected exit, operation never finished bootstrapping - no restart will be attempted}

Testing failed:
	Test target WebDriverAgentRunner encountered an error (Early unexpected exit, operation never finished bootstrapping - no restart will be attempted)
```
这是因为开发者没有在设备上被信任，尝试在设备上手动运行 `WebDriverAgentRunner` 应用，
会弹出一条消息：

![Untrusted developer](../../en/drivers/ios-xcuitest-img/untrusted-dev.png)

在设备的 设置 => 通用 => 设备管理 里信任开发者以允许使用 `WebDriverAgentRunner` 应用。
(查看 [苹果文档获取更多信息](https://support.apple.com/en-us/HT204460))。

### 基础（手动）配置

很多情况下用基础自动配置还不够。为了在真机上运行测试一般还需要处理项目的签名和配置。一般在使用免费开发者账号
的时会出现这种情况，因为既不能创建通配符 provisioning profile，也不会给默认应用包创建。

会有这种报错 Xcode **failed to create provisioning profile**

![No provisioning profile](../../en/drivers/ios-xcuitest-img/no-prov-prof.png)

简单的处理方法是打开 [Xcode](https://developer.apple.com/xcode/) 新建一个项目并创建
provisioning profile：

![Create new project](../../en/drivers/ios-xcuitest-img/create-new-project.png)

"iOS" 下的什么类型都行。最简单的是 "Single View Application"：

![Create single page](../../en/drivers/ios-xcuitest-img/create-single-page.png)

重要的是使用唯一的 "Product Name" 和 "Organization Name"。还有选择你的 "Team"。

![Setup bundle](../../en/drivers/ios-xcuitest-img/set-up-bundle.png)

在 "Project" 标签里可以确认 provisioning profile 有没有创建。

![Project pane](../../en/drivers/ios-xcuitest-img/project-prov-prof.png)

也可以在账户设置查看 provisioning profile：

![Check provisioning profile](../../en/drivers/ios-xcuitest-img/check-prov-prof.png)

现在就有有效的 provisioning profile 了。把 bundle id 填在你测试项目的 `updatedWDABundleId` desired
capability 里。然后再按照 [initial instructions for automatic configuration](#basic-automatic-configuration) 做。


### 全手动配置

也可以手动关联项目和 provisioning profile（请记得每次升级 WebDriverAgent 以及安装 Appium
新版本之后都需要重新配置一遍，不建议用这种方式）：

*   查找 Appium 安装在哪里：
```
    $ which appium
    /path/where/installed/bin/appium
```
*   如果路径是 `/path/where/installed/bin/appium`，`WebDriverAgent` 项目会在 `/path/where/installed/lib/node_modules/appium/node_modules/appium-webdriveragent`。
    在终端进入这个路径，执行以下命令完成项目设置：
```
    mkdir -p Resources/WebDriverAgent.bundle
    ./Scripts/bootstrap.sh -d
```
*   用 Xcode 打开 `WebDriverAgent.xcodeproj`，分别在 `WebDriverAgentLib` 和 `WebDriverAgentRunner`
    targets 的 "General" 选项卡里勾选 "Automatically manage signing"，并选上你的 `Development Team`。
    然后会自动选上 `Signing Ceritificate`。看起来应该如下图：

    ![WebDriverAgent in Xcode project](../../en/drivers/ios-xcuitest-img/xcode-config.png)

    * Xcode 给 `WebDriverAgentRunner` 创建 provisioning profile 的时候可能会失败：

      ![Xcode provisioning fail](../../en/drivers/ios-xcuitest-img/xcode-facebook-fail.png)

    * 需要手动在 "Build Settings" 选项卡修改 target 的 bundle id，并且把 "Product Bundle Identifier"
      从 `com.facebook.WebDriverAgentRunner` 改为 Xcode 可以通过的内容：

      ![Xcode bundle id](../../en/drivers/ios-xcuitest-img/xcode-bundle-id.png)

    * 回到 "General" 选项卡的 `WebDriverAgentRunner` target，现在应该看到它创建了
      provisioning profile 并且一切正常：

      ![Xcode provisioning profile](../../en/drivers/ios-xcuitest-img/xcode-facebook-succeed.png)

*   最后，验证下是否可以正常运行。编译项目：
```
    xcodebuild -project WebDriverAgent.xcodeproj -scheme WebDriverAgentRunner -destination 'id=<udid>' test
```
如果编译成功，应该输出如下内容：
```
    Test Suite 'All tests' started at 2017-01-23 15:49:12.585
    Test Suite 'WebDriverAgentRunner.xctest' started at 2017-01-23 15:49:12.586
    Test Suite 'UITestingUITests' started at 2017-01-23 15:49:12.587
    Test Case '-[UITestingUITests testRunner]' started.
        t =     0.00s     Start Test at 2017-01-23 15:49:12.588
        t =     0.00s     Set Up
```
*   为了完全验证，可以尝试访问 WebDriverAgent 服务状态（**注意：** 你必须和设备在同一个网络，
    并且知道设备的 IP 地址，可以在 设置 => Wi-Fi => 连接中的网络 查看）：

```
    export DEVICE_URL='http://<device IP>:8100'
    export JSON_HEADER='-H "Content-Type: application/json;charset=UTF-8, accept: application/json"'
    curl -X GET $JSON_HEADER $DEVICE_URL/status
```
    应该看到输出如下返回：
```
    {
      "value" : {
        "state" : "success",
        "os" : {
          "name" : "iOS",
          "version" : "10.2"
        },
        "ios" : {
          "simulatorVersion" : "10.2",
          "ip" : "192.168.0.7"
        },
        "build" : {
          "time" : "Jan 23 2017 14:59:57"
        }
      },
      "sessionId" : "8951A6DD-F3AD-410E-A5DB-D042F42F68A7",
      "status" : 0
    }
```

### 配置待测 App

除了 WebDriverAgent，为了在设备上运行，你的 App 也需要配置好。主要要求是一样的：用开发
provisioning profile build 的 App（`.ipa` 文件）。[这里](https://medium.com/ios-os-x-development/ios-code-signing-provisioning-in-a-nutshell-d5b247760bef#.5hirl92tn)有一个不错的流程概述，还有
[这里](https://www.nodesagency.com/understanding-code-signing-for-ios-apps)。

再详细的说，为了使用真机，你需要：

* [Apple Developer ID](https://developer.apple.com/programs/ios/) 和配置好开发者证书
和 provisioning profile 的有效的开发者账号。
* 在真机上测试有效的 iOS 开发证书和 Provisioning Profile 是必要的。你的 App 也需要被签名。在 [Apple documentation](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/TestingYouriOSApp/TestingYouriOSApp.html) 可以找到相关信息。
* 一个配置好可以在 Xcode 里开发用的 iPad 或者 iPhone。
* 一个签过名的 `.app` 或者 `.ipa` 文件，或者从源码 build 一个。
* 一台有 [Xcode](https://developer.apple.com/xcode/) 和 Xcode Command Line Developer Tools
的 Mac。

Appium 用 `ideviceinstaller` (作为 `libimobiledevice` 的一部分被安装) 把应用安装到设备上。
不过有时候预先用 Xcode 安装 App 会更容易确认有没有问题（再看看 [Apple documentation](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/TestingYouriOSApp/TestingYouriOSApp.html)。

### 排障方法

1. 通过 Xcode 的 Organizer 或者 iTunes 确认 UDID 是否正确。UDID 是一长串字符（20 个字符以上）。
2. 确认你的测试可以在模拟器上执行。
3. 确认以下设置在你的设备上是**启用**的：
    1. 设置 -> 开发者 -> **Enable UI Automation**
    2. 设置 -> Safari 浏览器 -> 高级 -> **网页检查器** 和 **远程自动化**
        1. 请阅读 [Automating mobile web apps](/writing-running-appium/web/mobile-web) 了解更多关于 WebView 的细节。
4. 如果你不想为了手工配置生成使用通配符的 provisioning profile ，可以考虑使用 `.xctrunner` 作为 identifier。从 Xcode 11 开始支持了 `.xctrunner` 配置，[参考](https://github.com/appium/appium/issues/13610)。
5. 确认设备没有越狱
    - 设备上管理应用的服务 `com.apple.mobile.installation_proxy` 会[无法工作](https://github.com/appium/appium-desktop/issues/1447)。
