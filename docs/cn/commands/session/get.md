# 获取会话（session）的 Capabilities

取得指定会话（session）的capabilities参数

## 使用样例

```java
// Java
Map<String, Object> caps = driver.getSessionDetails();

```

```python
# Python
desired_caps = self.driver.desired_capabilities

```

```javascript
// Javascript
// webdriver.io example
let caps = driver.capabilities;

// wd example
let caps = await driver.sessionCapabilities();

```

```ruby
# Ruby
# ruby_lib example
session_capabilities

# ruby_lib_core example
@driver.session_capabilities

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
ICapabilities caps = driver.Capabilities;

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
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/server/ActiveSessions.html#get-org.openqa.selenium.remote.SessionId-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.desired_capabilities) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L227) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium%2FWebDriver%2FRemote%2FOSS%2FBridge:session_capabilities) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API规范

### 终端

`GET /session/:session_id`

### URL参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|

### JSON参数

None

### Response

一个描述会话（session）的capabilities 参数的对象(`object`)

## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionid)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019