# 屏幕截图

对当前的视窗（viewport）、窗口（window）、页面（page）进行截图

## 使用样例

```java
// Java
File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);

```

```python
# Python
screenshotBase64 = self.driver.get_screenshot_as_base64()

```

```javascript
// Javascript
// webdriver.io example
let screenshot = driver.takeScreenshot();

// wd example
let screenshot = await driver.takeScreenshot();

```

```ruby
# Ruby
# ruby_lib example
driver.screenshot_as(:base64) # via core_lib

# ruby_lib_core example
@driver.screenshot_as(:base64)

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
Screenshot screenshot = driver.GetScreenshot();

```

## 描述

在原生环境（iOS、Android）中获取视窗（viewport）的屏幕截图，在web环境中获取窗口（window）的屏幕截图

需要注意的是，一些平台基于安全原因可能会有防止获取屏幕截图的设置。[Android FLAG_SECURE layout parameter](https://developer.android.com/reference/android/view/WindowManager.LayoutParams.html#FLAG_SECURE)就是一个这样类型的功能。

## 支持

### Appium Server

| 平台    | Driver                                                   | 平台版本   | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/RemoteWebDriver.html#getScreenshotAs-org.openqa.selenium.OutputType-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.get_screenshot_as_base64) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1089) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Base/TakeScreenshot#screenshot_as-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API 规范

### 终端

`GET /session/:session_id/screenshot`

### URL参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|

### JSON参数

None

### 响应

使用base64编码的PNG格式的屏幕截图 (`string`)

## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#dfn-take-screenshot)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidscreenshot)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019