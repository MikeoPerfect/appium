# 设置脚本超时时间

为通过[execute async](/docs/en/commands/session/timeouts/async-script.md)方法执行的异步脚本设置允许执行的时间，以毫秒为单位。（仅限web环境）

## 使用样例

```java
// Java
driver.manage().timeouts().setScriptTimeout(30, TimeUnit.SECONDS);

```

```python
# Python
self.driver.set_script_timeout(5000)

```

```javascript
// Javascript
// webdriver.io example
driver.setAsyncTimeout(5000)

// wd example
await driver.setAsyncScriptTimeout(5000);

```

```ruby
# Ruby
# ruby_lib example
script_timeout(5) # Ruby translates it to seconds

# ruby_lib_core example
@driver.script_timeout(5) # Ruby translates it to seconds

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
// TODO C# sample

```

## 支持


### Appium Server

| 平台    | Driver                                                   | 平台版本 | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | None | None | None |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | None | None | None |
|  | [Espresso](/docs/en/drivers/android-espresso.md) | None | None | None |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | None | None | None |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | None | None | None |

### Appium 客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebDriver.Timeouts.html#setScriptTimeout-long-java.util.concurrent.TimeUnit-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.set_script_timeout) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L699) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Timeouts#script_timeout=) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/timeouts/async_script`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

| 名称 | 类型     | 描述                                 |
|----|----|-----------|
| ms | `number` | 运行有时间限制的命令的时间量（毫秒） |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidtimeoutsasync_script)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 79c66dcf34387f9b77f0ffb1695531e457e4d1dc, 13 Apr 2019