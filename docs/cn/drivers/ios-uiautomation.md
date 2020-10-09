## iOS的UIAutomation驱动

> **注意**: 此驱动已经过时且不应该被使用除非有必要。 此文档中的信息可能不最新
>结合实际情况，该驱动程序将在Appium的未来版本中删除。
> 当前开始使用Appium进行ios自动化，请使用 [XCUITest
> Driver](/docs/cn/drivers/ios-xcuitest.md) 替代.

Appium以前用于iOS应用程序自动化的方法是基于“UIAutomation”（UIAutomation是苹果在iOS 10之前iOS SDK附带的框架，后续ios版本已被移除）
UIAutomation是一个包含苹果的仪器分析系统，并提供了同步运行的单个应用程序上下文JavaScript API。
Appium UIAutomation驱动程序建立了一套异步的，基于会话的WebDriver前端API。


有关UIAutomation 驱动到
[appium-ios-driver](https://github.com/appium/appium-ios-driver) 了解更多

### 要求和支持

除了Appium的一般要求之外的要求：

* Xcode 版本小于或等于7.
* iOS 仿真器 或 设备 版本小于等于9.3.
* 所有版本的Appium附带本驱动
* 为了使驱动程序正常工作，请参见下面的其他设置。

### 用法


通过设置您的[新会话请求]（＃TODO）中的`platformName` [参数]（＃TODO）的值为iOS来使用UIAutomation驱动程序启动会话。当然，您至少还必须配置合适的`platformVersion`，`deviceName`和`app`参数。


### 功能

UIAutomation驱动程序支持许多Appium的标准功能 [Appium
功能](/docs/cn/writing-running-appium/caps.md), 但还有一个额外的
仅适用于该驱动程序的一组功能 (查看 [iOS
部分](/docs/cn/writing-running-appium/caps.md#ios-only) 
的前述文件).


要想自动使用Safari而不是你自己的应用程序，请将“app”功能设置为空，而将“browserName”功能设置为“Safari”。
### 命令

要查看Appium支持的各种命令，特别是关于命令如何映射到UIAutomation驱动程序的行为的信息，请参见 [API
相关](#TODO).

### 模拟器配置

(注意，由于Xcode和iOS模拟器的限制，在任何给定的时间，只能有一个模拟器是开放的，并且是自动的。对于多模拟器支持，您将需要升级到 [XCUITest 驱动](ios-xcuitest.md)).

1. 要让仪器实现iOS模拟器的自动化，你需要修改系统的授权数据库。Appium通过安装和运行授权脚本提供了一种简单的方法：
    ```
    sudo authorize-ios
    ```

1. 默认情况下，基于仪器的自动化受到指令之间1秒硬编码延迟的限制，这是由苹果的工程师出于不明原因做的。有一种方法可以绕过这个限制
   [instruments-without-delay](https://github.com/facebookarchive/instruments-without-delay)
   (IWD). IWD为小于7的Xcode附带提供Appium。Xcode为7或者以上的，在使用Appium之前，用户必须手动安装IWD。安装步骤如下：

    * 克隆 [appium-ios-driver](https://github.com/appium/appium-ios-driver)仓库
    * 在仓库内，运行bin目录中包含的xcode-iwd.sh脚本，
      向它传递几个参数：
      （1）您使用的Xcode应用程序的路径。 
      （2）appium-instruments文件夹的路径。例如： 
        ```
        sh ./bin/xcode-iwd.sh /Applications/Xcode.app /Users/me/appium-instruments/
        ```

1. 为了获得最佳结果，请启动您要使用的每个模拟器，并确保以下各项：

    * 启用了软键盘（Simulator应用程序中的Command + K）
    * UIAutomation 开启了开发者设置选项
    * 在Xcode的“Devices”管理器中不存在具有相同名称的多个模拟器

### 真实设备配置

由于代码签名和对苹果限制的额外变通，在真实设备上运行测试要复杂得多。使用此驱动程序成功实现自动化策略的基本过程如下：

1. 在您将运行测试的特定类型的真实设备上，使用调试配置构建您的应用程序，确保在您的特定设备上运行的应用程序已经进行了签名。例如：

    ```
    xcodebuild -sdk <iphoneos> -target <target_name> -configuration Debug \
        CODE_SIGN_IDENTITY="iPhone Developer: Mister Smith" \
        PROVISIONING_PROFILE="XXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX"
    ```

1. 将构建的应用程序(通常位于Xcode中指定的构建目录中)安装到您自己的测试设备上，确保它存在于设备上，并且没有签名错误。在设备上安装应用程序有很多方法。一是只使用Xcode本身。另一个是使用“ideviceinstaller”工具（“libimobiledevice”套件的一部分）。第三种是使用[ios-deploy](https://npmjs.org/package/ios-deploy)。这是一个关于`ideviceinstaller`的例子：

    ```
    # 首次安装ideviceinstaller, 使用 Homebrew (http://brew.sh)
    brew install libimobiledevice
    ideviceinstaller -u <UDID of your device> -i <path to your built app>
    ```

1. 使用你的应用程序的bundle ID作为`app`参数的值。
1. 使用UUID作为你的设备的`udid`参数的值。
1. 如上所述，确保在Developer设置中开启了UI Automation。 

遵循这些步骤应该能确保你的运行成功!如果你使用的是更新版本的Xcode(例如7.x)，您可能希望咨询[XCUITest
Driver Real Device Docs](/docs/cn/drivers/ios-xcuitest-real-devices.md)，他们可能包含更多相关的信息。

### 真实设备 Hybrid / Web Testing

对混合和web的测试,Appium需要使用“远程调试协议”去发送JavaScript，在网络视图中执行。对于真正的iOS设备，
此协议已加密，必须使用第三方工具来访问。由Google提供的工具称为
[ios-webkit-debug-proxy](https://github.com/google/ios-webkit-debug-proxy)
（IWDP）。有关在Appium中安装和使用IWDP的信息，请参阅
[IWDP doc](/docs/cn/writing-running-appium/web/ios-webkit-debug-proxy.md).

对于web测试，即在Safari浏览器中运行的测试，我们还需要跨越另一个障碍。在真实的设备上，没有开发者签名的应用程序不能被UIAutomation识别，例如Safari就是这样一个应用。因此，我们有一个名为“SafariLauncher”的助手应用，它可以由开发者签名。它在启动时的唯一目的是返回并启动Safari，然后通过远程调试器结合IWDP实现自动化。不幸的是，在这种情况下，您不能转移到本地上下文中并对浏览器本身进行任何自动化操作。


更多有关 `SafariLauncher`的设置信息, 请查阅 [SafariLauncher
doc](/docs/cn/drivers/ios-uiautomation-safari-launcher.md).

### 文件生成和 iOS 测试执行

在iOS上进行测试所生成的文件有时可能会很大。这些包括
日志，临时文件和Xcode运行的派生数据。一般从下面的位置找到它们并根据需要删除：

```
$HOME/Library/Logs/CoreSimulator/*
/Library/Caches/com.apple.dt.instruments/*
```

### 通过Jenkins运行 iOS 测试

首先下载`jenkins-cli.jar`并验证Mac是否成功
连接到Jenkins主节点。确保已运行上文提到的ʻauthorize-ios`命令。
```
wget https://jenkins.ci.cloudbees.com/jnlpJars/jenkins-cli.jar

java -jar jenkins-cli.jar \
 -s https://team-appium.ci.cloudbees.com \
 -i ~/.ssh/id_rsa \
 on-premise-executor \
 -fsroot ~/jenkins \
 -labels osx \
 -name mac_appium
```

接下来为Jenkins定义一个LaunchAgent，在登录时自动启动。
LaunchDaemon无法使用，因为守护程序没有GUI访问权限。确保
plist不包含“ SessionCreate”或“ User”键，因为这可能会阻止
测试运行。当配置错误的时候，您会看到“无法授权权限”错误。

```
$ sudo nano /Library/LaunchAgents/com.jenkins.ci.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.jenkins.ci</string>
    <key>ProgramArguments</key>
    <array>
        <string>java</string>
        <string>-Djava.awt.headless=true</string>
        <string>-jar</string>
        <string>/Users/appium/jenkins/jenkins-cli.jar</string>
        <string>-s</string>
        <string>https://instructure.ci.cloudbees.com</string>
        <string>on-premise-executor</string>
        <string>-fsroot</string>
        <string>/Users/appium/jenkins</string>
        <string>-executors</string>
        <string>1</string>
        <string>-labels</string>
        <string>mac</string>
        <string>-name</string>
        <string>mac_appium</string>
        <string>-persistent</string>
    </array>
    <key>KeepAlive</key>
    <true/>
    <key>StandardOutPath</key>
    <string>/Users/appium/jenkins/stdout.log</string>
    <key>StandardErrorPath</key>
    <string>/Users/appium/jenkins/error.log</string>
</dict>
</plist>
```


最后设置所有者，权限，然后启动代理。

```
sudo chown root:wheel /Library/LaunchAgents/com.jenkins.ci.plist
sudo chmod 644 /Library/LaunchAgents/com.jenkins.ci.plist

launchctl load /Library/LaunchAgents/com.jenkins.ci.plist
launchctl start com.jenkins.ci
```
