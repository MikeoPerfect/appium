# 设置超时

为特定类型的操作执行配置时间量，超过时间后操作会被终止。

## 使用样例

```java
// Java
driver.manage().timeouts().pageLoadTimeout(30, TimeUnit.SECONDS);

```

```python
# Python
self.driver.set_page_load_timeout(5000)

```

```javascript
// Javascript
// webdriver.io example
driver.setTimeouts(5000)

// wd example
await driver.setPageLoadTimeout(5000);

```

```ruby
# Ruby
# ruby_lib example
timeout('pageLoad', 5) # Ruby translates it to seconds

# ruby_lib_core example
@driver.timeout('pageLoad', 5) # Ruby translates it to seconds

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.Manage().Timeouts().PageLoad = TimeSpan.FromSeconds(30);

```


## 描述

超时类型可以是“页面加载”，“脚本”和“隐式等待”。（使用样例中仅展示了“页面加载”）

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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/RemoteWebDriver.RemoteWebDriverOptions.RemoteTimeouts.html#pageLoadTimeout-long-java.util.concurrent.TimeUnit-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.set_page_load_timeout) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L714) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Remote/OSS/Bridge#timeout-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/ITimeouts.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/timeouts`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

| 名称 | 类型     | 描述                                                         |
|----|----|-----------|
| type | `string` | 要设置超时的操作类型。有效的值包括：`script`为脚本类型超时，`implicit`修改隐式等待的超时，`page load`设置页面加载的超时。 |
| ms | `number` | 运行有时间限制的命令的时间量（毫秒） |


### 响应

null


## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#set-timeouts)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidtimeouts)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: a11f693bbe2bcf2e47fa6a40872a7580ab45d6bb, 6 Jun 2020