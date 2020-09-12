# 设置显示方向

设置设备/浏览器当前的显示方向

## 使用样例

```java
// Java
driver.rotate(ScreenOrientation.LANDSCAPE);

```

```python
# Python
driver.orientation = "LANDSCAPE"

```

```javascript
// Javascript
// webdriver.io example
driver.setOrientation("LANDSCAPE");

// wd example
await driver.setOrientation('LANDSCAPE');

```

```ruby
# Ruby
# ruby_lib example
rotation = :landscape

# ruby_lib_core example
@driver.rotation = :landscape

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.Orientation = ScreenOrientation.Landscape;

```

## 支持


### Appium Server

| 平台    | Driver                                                   | 平台版本   | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium 客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/Rotatable.html#rotate-org.openqa.selenium.DeviceRotation-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.orientation) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L2042) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/DriverExtensions/Rotatable:orientation) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/blob/master/src/Appium.Net/Appium/AppiumDriver.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/orientation`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

| 名称         | 类型     | 描述                                       |
|----|----|-----------|
| orientation | `string` | 想要设置的显示方向，两个值可选：{LANDSCAPE（横屏）\| PORTRAIT（竖屏） |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#post-sessionsessionidorientation)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: a11f693bbe2bcf2e47fa6a40872a7580ab45d6bb, 6 Jun 2020