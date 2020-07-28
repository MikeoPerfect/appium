## Android的Espresso驱动

Appium目前通过自己的Espresso驱动程序支持[Espresso](https://developer.android.com/training/testing/espresso/index.html)自动化技术。这个驱动程序通过启动设备上运行的Espresso来工作，并将我们自己的自动化服务器作为Espresso测试APK的一部分。在此基础上，Appium可以与此自动化服务器进行通信，并且通过Appium客户端调用触发Espresso命令。

Espresso驱动的发展是发生在[appium-espresso-driver](https://github.com/appium/appium-espresso-driver)的回购。

Appium也支持Android自动化通过使用[UiAutomator2 Driver](/docs/en/drivers/android-uiautomator2.md).)

### 要求和支持

除了Appium的一般要求外，还需要具备以下条件:

* Java 7需要被正确安装和配置在你的平台上
* 具备能运行Android SDK的Mac, Windows, 或者Linux OS 

### 使用

使用Espresso驱动程序启动会话的方法是在的[新的会话请求](#TODO)中的[capability](#TODO)参数设置中需要包含属性为`automationName` ,对应的值为 `Espresso`。当然了，capabilities的参数设置中中还必须至少包含有正确的`platformName` (=`Android`), `platformVersion`, `deviceName`, 和 `app`这些参数信息。

### Capabilities

Espresso驱动程序当前支持标准[Android capabilities](/docs/en/writing-running-appium/caps.md#android-only)的子集。

### 设置

安装Espresso驱动程序基本上需要准备好Android SDK和构建工具。你可以参照UiAutomator2驱动程序文档[UiAutomator2 Driver文档](android-uiautomator2.md#basic-setup) ，因为这些步骤都是一样的。