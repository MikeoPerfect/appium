# 创建新的会话（session）

创建一个新的会话（session）
## 使用样例

```java
// Java
DesiredCapabilities desiredCapabilities = new DesiredCapabilities();
desiredCapabilities.setCapability(MobileCapabilityType.PLATFORM_VERSION, "10.3");
desiredCapabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "iPhone Simulator");
desiredCapabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, "XCUITest");
desiredCapabilities.setCapability(MobileCapabilityType.APP, "/path/to/ios/app.zip");

URL url = new URL("http://127.0.0.1:4723/wd/hub");

IOSDriver driver = new IOSDriver(url, desiredCapabilities);
String sessionId = driver.getSessionId().toString();

```

```python
# Python
desired_caps = {
  'platformName': 'Android',
  'platformVersion': '7.0',
  'deviceName': 'Android Emulator',
  'automationName': 'UiAutomator2',
  'app': PATH('/path/to/app')
}
self.driver = webdriver.Remote('http://127.0.0.1:4723/wd/hub', desired_caps)

```

```javascript
// Javascript
// webdriver.io example
let options = { desiredCapabilities: {
  platformName: 'Android',
  platformVersion: '7.0',
  automationName: 'UiAutomator2',
  app: path.resolve('path', 'to', 'app.apk')
}};
let client = driver.newSession(options);

// wd example
let driver = await wd.promiseChainRemote({
  host: '127.0.0.1',
  port: 4723
});
let desiredCaps = {
  platformName: 'Android',
  platformVersion: '7.0',
  deviceName: 'Android Emulator',
  app: path.resolve('path', 'to', 'app.apk')
};
await driver.init(desiredCaps);

```

```ruby
# Ruby
# ruby_lib example
APP_PATH = '../../path/to/app.app'

desired_caps = {
  caps: {
    platformName:  'iOS',
    platformVersion: '10.2',
    deviceName:    'iPhone 6',
    app:           APP_PATH,
    automationName: "XCUITest"
  }
}

Appium::Driver.new(desired_caps).start_driver

# ruby_lib_core example
::Appium::Core.for(desired_caps).start_driver

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
AppiumOptions capabilities = new AppiumOptions();
appiumOptions.AddAdditionalCapability(MobileCapabilityType.PlatformName, "Android");
appiumOptions.AddAdditionalCapability(MobileCapabilityType.PlatformVersion, "7.1.1");
appiumOptions.AddAdditionalCapability(MobileCapabilityType.DeviceName, "Android Device");
appiumOptions.AddAdditionalCapability("appPackage", "com.instagram.android");
appiumOptions.AddAdditionalCapability("appActivity", "com.instagram.android.activity.MainTabActivity");

AndroidDriver<AndroidElement> driver = new AndroidDriver<AndroidElement>(new Uri("http://127.0.0.1:4723/wd/hub"), appiumOptions);

```

## 描述

服务器应尝试创建一个与desired capabilities以及Required capabilities中各项最匹配的会话。

* [JSONWP规范](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#session-1) Required capabilities比desired capabilities有更高的优先级，并且创建会话（session）时Required capabilities必须被设置。
* [W3C 规范](https://www.w3.org/TR/webdriver/#dfn-new-session) capabilities.alwaysMatch在创建会话（session）时必须被设置; capabilities.firstMatch 必须匹配至少一项 (第一个匹配项会被使用)

## 支持

### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium客户端

|语言|支持版本|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/server/DefaultSession.html#createSession-org.openqa.selenium.remote.server.DriverFactory-org.openqa.selenium.remote.server.Clock-org.openqa.selenium.remote.SessionId-org.openqa.selenium.Capabilities-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webelement.WebElement.clear) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1780) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Element:clear) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API规范

### 终端

`POST /session`

### URL参数

None

### JSON参数

|名称|类型|描述|
|----|----|-----------|
| desiredCapabilities | `object` | ([JSONWP 规范](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#session-1)) 对象， 描述创建会话所需的 [desired capabilities](/docs/en/writing-running-appium/caps.md) |
| requiredCapabilities | `object` | ([JSONWP 规范](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#session-1)) 对象，描述创建会话所需的 required capabilities， 一定被移动端应用 |
| capabilities | `object` | ([W3C 规范](https://www.w3.org/TR/webdriver/#dfn-new-session)) 对象，包含'alwaysMatch' and 'firstMatch' 属性 |
| capabilities.alwaysMatch | `object` | 移动端必须匹配的[desired capabilities](/docs/en/writing-running-appium/caps.md) |
| capabilities.firstMatch | `array<object>` | capabilities的数组，移动端会尝试在其中进行匹配。 匹配数组中的第一个。 |

### 响应

一个描述会话（session）的 capabilities的对象 (`object`)

## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#dfn-new-session)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#session-1)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 1be5bd8c1e22fe46188dd9c498766ae587c88887, 4 Mar 2020