## iOS XCUITest 驱动

Appium 通过 `XCUITest` 驱动支持基本的 iOS 应用自动化。_(Appium 新手? 读一读 [介绍 Appium 驱动](#TODO))_。它在底层使用 [XCUITest](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/09-ui_testing.html) 库以更好的自动化你的 App。 对 XCUITest 的使用是通过 [WebDriverAgent](https://github.com/facebook/webdriveragent) 服务间接完成的。
WebDriverAgent (也被叫做"WDA") 是 Facebook 管理的项目, Appium 核心团队对项目做了很大的贡献。 WDA是一个运行在 iOS 模拟器或设备上暴露 XCUITest API 的服务，兼容 WebDriver。Appium 的 XCUITest 驱动把 WDA 作为对 Appium 用户不透明的子进程控制， 代理发送给和接受自 WDA 的命令， 并且提供大量额外功能 (比如模拟器控制及其他方法)。
XCUITest 驱动的开发在 [appium-xcuitest-driver](https://github.com/appium/appium-xcuitest-driver) 仓库进行。

### 依赖和支持

除了 Appium 通用依赖以外的要求：

* 苹果的 XCUITest 库只能运行在 iOS 9.3 及以上的版本的模拟器或设备上。
* 安装 macOS 10.11 或 10.12 的 Mac 电脑。
* Xcode 7 及以上的版本。
* Appium 在 1.6 及以上的版本才提供 XCUITest 驱动。
* 需要额外的系统库驱动才能正常工作(查看下面的安装分节)。


### 从 UIAutomation 驱动迁移

如果需要从 Appium 的旧 [UIAutomation-based 驱动](/docs/cn/drivers/ios-uiautomation.md) 迁移到 XCUITest 驱动，可以查阅[迁移指南](/docs/cn/advanced-concepts/migrating-to-xcuitest.md)。

### 用法

使用 XCUITest 驱动建立会话需要在[新会话请求](#TODO)里包含值为 `XCUITest` 的 `automationName` [capability](#TODO)。当然最少也要包含恰当的`platformName`，`platformVersion`，`deviceName`，和 `app` capabilities。

iPhone 或 iPad 的 `platformName` 应该是 `iOS`。tvOS 设备的 `platformName` 应该是 `tvOS`。

- iOS
   ```json
   {
      "automationName": "XCUITest",
      "platformName": "iOS",
      "platformVersion": "12.2",
      "deviceName": "iPhone 8",
      ...
   }
   ```
- tvOS
   ```json
   {
      "automationName": "XCUITest",
      "platformName": "tvOS",
      "platformVersion": "12.2",
      "deviceName": "Apple TV",
      ...
   }
   ```

### Capabilities

XCUITest 驱动除了支持许多标准 [Appium capabilities](/docs/cn/writing-running-appium/caps.md)，还有一组额外的 capabilities 调整驱动的行为。可以在 [appium-xcuitest-driver README](https://github.com/appium/appium-xcuitest-driver#desired-capabilities) 查看。

如果要自动化 Safari 而不是自有的应用，`app` capability 留空，设置 `browserName` capability 为 `Safari`。

### 命令

查看 Appium 支持的各种命令，特别是关于命令如何映射到 XCUITest 驱动行为的信息，请参阅 [API 参考](#TODO)。


### 基本安装

_(我们建议使用 [Homebrew](https://brew.sh) 安装系统依赖)_

1. 确保已经安装配置了 Appium 通用依赖(比如 Node & NPM)。
2. 安装 [Carthage](https://github.com/Carthage/Carthage):

    ```bash
    brew install carthage
    ```

如果你不需要在真机上自动运行就安好了！在模拟器上自动化应用，`app` capability 应该设为指向你的为模拟器构建的 `.app` 或 `.app.zip` 文件的绝对路径或链接。

### 真机安装

因为苹果对真机上运行的应用的严格限制，在真机上运行 XCUITest 自动化要复杂得多。请看 [XCUITest 真机安装文档](ios-xcuitest-real-devices.md)中的介绍。

安装完成后，通过使用以下 desired capabilitie 和真机建立会话：

* `app` 或 `bundleId` - 指定应用 (已签名 `.ipa` 文件的本地路径或链接)，如果应用已经安装，Appium 只要有应用的 bundle identifier 就可以启动它。
* `udid` - 指定运行测试的真机 id。如果只有一台设备也可以设为 `auto`，Appium 会确定设备和 id。

### 可选安装

* 安装 idb 可以更好的处理各种模拟器操作，比如生物识别，设置定位和窗口焦点。
   * 根据 https://github.com/appium/appium-idb#installation 安装必要的库 (Appium 1.14.0 以后)。

* 安装 [AppleSimulatorUtils](https://github.com/wix/AppleSimulatorUtils) 后可以使用 [permissions capability](https://github.com/appium/appium-xcuitest-driver#desired-capabilities)。

### 运行测试产生的文件

在 iOS 上测试产生的文件有时会占用很多空间，包括日志、临时文件和 Xcode 运行的派生数据。可以在以下路径删除它们：
```
$HOME/Library/Logs/CoreSimulator/*
$HOME/Library/Developer/Xcode/DerivedData/*
```

### 配置键盘
在 Appium 1.14.0 之后，为了让测试运行的更稳定 Appium 会重置键盘的设置为默认项。你可以通过设置 API 修改：

- 在 _键盘_ 关闭`自动改正`
- 在 _键盘_ 关闭`输入预测`
- 标记键盘教程为完全版
- (仅模拟器) 打开软键盘
