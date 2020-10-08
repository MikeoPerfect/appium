## 自动化测试移动端 web 应用

如果你有兴趣在 iOS 系统上的 Safari 浏览器或者 Android 系统上的 Chrome 浏览器进行网页自动化的话
，Appium可以帮到你。你只要正常地写 WebDriver 测试，通过对 desired capabilities 进行一些特殊的设置，可以把 Appium 当成 Selenium 服务来运行。

### iOS 移动 web 自动化

Appium 可以在真实或模拟的 iOS 设备上的 Safari 浏览器上进行自动化。通过将 [desired capabilty](/docs/cn/writing-running-appium/caps.md) 中的 `browserName` 的值设置为 `"Safari"` 同时将 `app` 功能留空。

在尝试运行 Appium 之前，你**必须**要先在设备上运行 Safari ，以确保相关参数已经被正确的设置。

然后，你就可以在移动端设备上的 Safari 浏览器上通过设置 desired capabilities 来运行你的测试。

```javascript
// javascript
{
  platformName: 'iOS'
  , platformVersion: '13.2'
  , automationName: 'XCUITest'
  , browserName: 'Safari'
  , deviceName: 'iPhone 11'
}
```

```python
# python
{
  'platformName': 'iOS',
  'platformVersion': '13.2',
  'automationName': 'XCUITest',
  'browserName': 'Safari',
  'deviceName': 'iPhone 11'
}
```

```php
// php
public static $browsers = array(
    array(
        'desiredCapabilities' => array(
            'platformName' => 'iOS',
            'platformVersion' => '13.2',
            'automationName' => 'XCUITest',
            'browserName' => 'Safari',
            'deviceName' => 'iPhone 11'
        )
    )
);
```

```java
// java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "iOS");
capabilities.setCapability(MobileCapabilityType.PLATFORM_VERSION, "13.2");
capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "XCUITest");
capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "Safari");
capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "iPhone 11");
```

```ruby
{
  platformName: 'iOS',
  platformVersion: '13.2',
  automationName: 'XCUITest',
  deviceName: 'iPhone 11',
  browserName: 'Safari'
}
```

### iOS 虚拟机上的移动端 Safari

首先，确定你的 Safari 开发者模式开启，移动调试端口打开。


### iOS 真机上的移动端 Safari

在 [iOS 9.3 及以下版本](/docs/cn/drivers/ios-uiautomation.md) (pre-XCUITest)版本系统，我们借助 [SafariLauncher App](https://github.com/snevesbarros/SafariLauncher) 应用在移动端 Safari 运行测试。
这是因为Safari是苹果公司的应用，Instruments 不能在真机上拉起 Safari。SafariLuncher 可以帮助打开 Safari 浏览器，浏览器一旦打开，Remote Debugger 会通过 [ios-webkit-debug-proxy](https://github.com/google/ios-webkit-debug-proxy) 自动连接。在 `ios-webkit-debug-proxy` 运行时，
必须在你的iOS设备测试前，对这台设备进行授权。

指导如何安装和运行 ios-webkit-debugger-proxy ，可以查阅 [iOS WebKit debug proxy](/docs/cn/writing-running-appium/web/ios-webkit-debug-proxy.md)

### 安装

在真实上运行测试前，你需要：

* 安装好 **ios-webkit-debug-proxy**，运行并在 27753 接口开启监听。（查阅 [hybrid 文档](/docs/cn/writing-running-appium/web/hybrid.md#execution-against-a-real-ios-device) 作为指导）
* 在 iOS 设备上开启 **web inspector**（设置>safari>高级）
* `XCUITest` 和 `Instruments`
	* 在 iOS 设备上开启 **web inspector**（设置>safari>高级）
* 只有 `Instruments`时
	* 安装好 **ios-webkit-debug-proxy**，运行并在 27753 接口开启监听。
		(详情见以下文档 [hybrid docs](/docs/cn/writing-running-appium/web/hybrid.md#execution-against-an-ios-real-device) )
	* 确保 `SafariLauncher` 能正常工作 
		(详情见以下文档 [SafariLauncher docs](/docs/cn/drivers/ios-uiautomation-safari-launcher.md) )

### 运行你的测试

在 Safari 运行你的测试，只需简单地设置 `"browserName"`  为 `"Safari"` 。

```java
// java
//设置web driver并启动 webview 应用。
DesiredCapabilities desiredCapabilities = new DesiredCapabilities();
desiredCapabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "Safari");
URL url = new URL("http://127.0.0.1:4723/wd/hub");
AppiumDriver driver = new AppiumDriver(url, desiredCapabilities);

// 浏览网页和定位页面元素取得id。
driver.get("http://saucelabs.com/test/guinea-pig");
WebElement div = driver.findElement(By.id("i_am_an_id"));
Assert.assertEquals("I am a div", div.getText()); //检查检索到的文本是否与预期值匹配
driver.findElement(By.id("comments")).sendKeys("My comment"); //按 id 填充 comments 字段。

//关闭浏览器
driver.quit();
```

```python
# python
# 建立web driver，开启浏览器app。
capabilities = { 'browserName': 'Safari', 'automationName': 'XCUITest' }
driver = webdriver.Remote('http://localhost:4723/wd/hub', capabilities)

# 浏览网页和定位页面元素取得id。
driver.get('http://saucelabs.com/test/guinea-pig');
div = driver.find_element_by_id('i_am_an_id')
# 检查文本是否匹配值
assertEqual('I am a div', div.text)

#  通过元素id填值。
driver.find_element_by_id('comments').send_keys('My comment')

# 关闭浏览器。
driver.quit()
```

```php
// php
class ContextTests extends PHPUnit_Extensions_AppiumTestCase
{
    public static $browsers = array(
        array(
            'desiredCapabilities' => array(
                'platformName' => 'iOS',
                'platformVersion' => '7.1',
                'automationName' => 'XCUITest',
                'browserName' => 'Safari',
                'deviceName' => 'iPhone 11'
            )
        )
    );

    public function testThings()
    {
        $this->get('http://saucelabs.com/test/guinea-pig');

        $div = $this->byId('i_am_an_id');
        $this->assertEquals('I am a div', $div->text());

        $this->byId('comments')->sendKeys('My comment');
    }
}
```


### Android 移动 web 自动化

无论是在真实还是模拟的 Android 设备上，Appium 都支持 Chrome 浏览器的自动化。

先决条件：

*确保 Chrome 浏览器已经安装在你的真实或虚拟的安卓设备上。
*需要安装好ChromeDriver（来自 Appium 的默认版本）
	并且配置好用于自动化设备上可用的特定版本的 Chrome 。点击 [这里](/docs/en/writing-running-appium/web/chromedriver.md) 去了解更多关于兼容性的详细信息。

然后使用 [desired capabilties](/docs/cn/writing-running-appium/caps.md) 像下面的例子去 Chrome 浏览器上运行你的测试。

```javascript
// javascript
{
  platformName: 'Android'
  , platformVersion: '9.0'
  , deviceName: 'Android Emulator'
  , automationName: 'UIAutomator2'
  , browserName: 'Chrome'
};
```

```python
# python
{
  'platformName': 'Android',
  'platformVersion': '9.0',
  'deviceName': 'Android Emulator',
  'automationName': 'UIAutomator2',
  'browserName': 'Chrome'
}
```

```php
// php
public static $browsers = array(
    array(
        'desiredCapabilities' => array(
            'platformName' => 'Android',
            'platformVersion' => '9.0',
            'browserName' => 'Chrome',
            'automationName' => 'UIAutomator2',
            'deviceName' => 'Android Emulator'
        )
    )
);
```

```java
// java
DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, "Android");
capabilities.setCapability(MobileCapabilityType.PLATFORM_VERSION, "9.0");
capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "Android Emulator");
capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "UIAutomator2");
capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, "Chrome");
```

```ruby
{
  platformName: 'Android',
  platformVersion: '9.0',
  deviceName: 'Android Emulator',
  automationName: 'UIAutomator2',
  browserName: 'Chrome'
}
```

注意：在 4.4+ 版本的设备上，你也可以将 `browserName` 设置为 'Browser' 在内建的浏览器上运行自动化。设置浏览器为 'Chromium' 是在所有设备可以运行的。在所有设备上，你可以将 `browserName` 设置为 'Chromium' 来对 Chromium 的某个版本进行自动化。

#### Chromedriver 的障碍排除

如果你的测试目标要求更新的 ChromeDriver 版本时，ChromeDriver 的这一特性 [chromedriver_自动下载](/docs/cn/writing-running-appium/web/chromedriver.md#automatic-discovery-of-compatible-chromedriver) 会帮到你。这一特性在 Appium 1.15.0的安全性选项中已经能够使用。你可以通过点击文件的链接去学习如何使用它。
当你需要特定版本的 ChromeDriver 时，`chromedriverExecutableDir` 这一功能能帮到你。

截止 Chrome Version 33，设备不再需要被 root。在这之前，设备需要被 root，因为 ChromeDriver 设置启动 Chrome 的命令行参数需要在 `/data/local` 目录的写入权限。

如果在 Chrome 低于 33 版本上测试，请确保 `adb shell` 有设备读取/写入 `/data/local` 权限。

```center
$ adb shell su -c chmod 777 /data/local
```

这里提及下 Chromedriver 有个功能 `showChromedriverLog`，当你将其设置为 `true`时，Appium 日志会一起写入 Chromedriver 日志中。这对我们的调试十分有帮助。

更多 chromedriver 文档参见(https://sites.google.com/a/chromium.org/chromedriver/getting-started/getting-started---android)

本文由 [CrazyForPoor](https://github.com/CrazyForPoor) 翻译。