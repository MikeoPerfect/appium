## Android的Espresso Driver

Appium目前是通过自身的Espresso driver支持[Espresso](https://developer.android.com/training/testing/espresso/index.html)自动化技术。driver是通过启动设备上运行的Espresso来工作，并将自己的自动化服务器作为Espresso测试APK的一部分。在此基础上，Appium可以与此自动化服务器进行通信，并且通过Appium客户端调用触发Espresso命令。

在[appium-espresso-driver](https://github.com/appium/appium-espresso-driver)的回购了Espresso driver后，该driver开始发展。

Appium也支持通过使用[UiAutomator2 Driver](/docs/en/drivers/android-uiautomator2.md)实现Android自动化。

### 要求和支持

除了Appium的一般要求外，还需要具备以下条件:

* Java 7正确安装和配置在你的测试平台上
* 具备能运行Android SDK的Mac, Windows, 或者Linux OS 

### 使用

使用Espresso driver启动会话的方法是在的[新的会话请求](#TODO)中的[capability](#TODO)参数设置中需要包含属性为`automationName` ,对应的值为 `Espresso`。当然了，capabilities的参数设置中还必须至少有正确的参数信息，包括`platformName` (=`Android`), `platformVersion`, `deviceName`, 和 `app`这些参数。

### Capabilities

Espresso driver当前支持标准的[Android capabilities](/docs/en/writing-running-appium/caps.md#android-only)。

### 设置

安装Espresso driver基本上需要准备好Android SDK和构建工具。你可以参照UiAutomator2驱动程序文档[UiAutomator2 Driver文档](android-uiautomator2.md#basic-setup) ，这些步骤都是一样的。
