
## Android的UiAutomator驱动

Appium对Android应用程序自动化的较早支持是通过`UiAutomator` driver实现的。_(New to Appium对Appium不熟悉? 请阅读 [Appium drivers介绍](#TODO))_。这个driver是利用了Google的[UiAutomator](https://developer.android.com/training/testing/ui-automator.html)技术实现了在设备上启动自动化。

在[appium-android-driver](https://github.com/appium/appium-android-driver) 的收购了UiAutomator driver后，driver开始发展。

我们建议您升级到 [UiAutomator2 Driver](android-uiautomator2.md)，并使用该driver，因为该driver的版本是向前兼容旧版本的。

### 要求和支持

除了Appium的一般要求外，还需要具备以下条件:

* Java 7正确安装和配置在你的测试平台上
* 具备能运行Android SDK的Mac, Windows, 或者Linux OS 

### 使用

使用UiAutomator driver启动会话的方法是在[新的会话请求](#TODO)的[capability](#TODO)参数中设置属性为`platformName`，对应的值为`Android`。当然了，capabilities的参数还必须包含有其他正确的参数信息，包括`platformName` (=`Android`), `platformVersion`, `deviceName`, 和 `app`这些参数。 在使用此driver时，对于低于`1.14.0`的Appium版本，无法使用`automationName`功能，而对于高于 `1.14.0` 和更高版本Appium的 `automationName`参数，应将其设置为 `UiAutomator1`。

强烈建议也设置`appPackage`和`appActivity`功能参数，以便让Appium确切知道为您的应用程序启动哪个包和activity。否则，Appium会尝试从您的应用清单中自动确定这些内容。

### Capabilities

 UiAutomator driver支持许多标准的[Appium capabilities](/docs/en/writing-running-appium/caps.md)，但也有一组额外的功能，这些功能可调节driver的行为。这些可以在前面提到的文档的[Android部分](https://github.com/testerhome/appium/blob/master/docs/en/writing-running-appium/caps.md#android-only)中找到。

对于web端的测试，如果要去自动化驱动Chrome而不是应用程序，则需要将`app` 功能参数保留为空，并且将`browserName`功能参数设置为 `Chrome`。请注意，您有责任确保Chrome是在模拟器/设备上，并且它的版本与Chromedriver兼容。


### 指令

需要查看Appium支持的各种命令，特别是关于命令如何映射到UiAutomator driver的行为的信息，请参阅[API参考](#TODO)。


### 设置

鉴于此driver与较新的UiAutomator2 driver的设置说明相同，请参阅[UiAutomator2 Driver](/docs/en/drivers/android-uiautomator2.md) 文档中的系统、仿真器和设备设置说明。
