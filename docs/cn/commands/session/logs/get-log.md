# 获得日志对象

获得给定日志类型的日志对象。在每次请求之后日志缓存被重置。

## 使用样例

```java
// Java
LogEntries logEntries = driver.manage().logs().get("driver");

```

```python
# Python
logs = driver.get_log('driver');

```

```javascript
// Javascript
// webdriver.io example
let logs = driver.getLogs('driver')

// wd example
const logs = await driver.log('driver');

```

```ruby
# Ruby
# ruby_lib example
get_log('driver')

# ruby_lib_core example
@driver.logs.get 'driver'

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
ILogs logs = driver.Manage().Logs;

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

### Appium 客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/logging/SessionLogs.html#getLogTypes--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html?highlight=get_log#selenium.webdriver.remote.webdriver.WebDriver.get_log) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L455) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib/Appium/Common#get_log-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/log`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

| 名称 | 类型     | 描述       |
|----|----|-----------|
| type | `string` | 日志的类型 |


### 响应

log entries的数组(`array<object>`)


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidlog)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019