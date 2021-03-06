[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
# 删除所有 Cookies

删除当前页面可见的所有cookies (仅是Web context)
[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
## 用法示例

```java
// Java
driver.manage().deleteAllCookies();

```

```python
# Python
self.driver.delete_all_cookies()

```

```javascript
// Javascript
// webdriver.io example
driver.deleteCookies();

// wd example
await driver.deleteAllCookies();

```

```ruby
# Ruby
# ruby_lib example
manage.delete_all_cookies

# ruby_lib_core example
@driver.manage.delete_all_cookies

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.Manage().Cookies.DeleteAllCookies();

```


[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
## 支持

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | None | None | None |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | None | None | None |
|  | [Espresso](/docs/en/drivers/android-espresso.md) | None | None | None |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | None | None | None |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | None | None | None |


[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### Appium Clients

|语言|支持版本|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/RemoteWebDriver.RemoteWebDriverOptions.html#deleteAllCookies--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.delete_all_cookies) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1993) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.selenium.dev](https://www.selenium.dev/documentation/en/support_packages/working_with_cookies/#delete-all-cookies) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Remote/RemoteCookieJar.cs) |

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
## HTTP API 规范

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### 路径

`DELETE /session/:sessionId/cookie`

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### JSON 参数

None

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
### 响应

null

[//]: # (DO NOT EDIT THIS FILE! This is an auto-generated file. Editing for this document happens in /commands-yml/commands/web/storage/delete-all-cookies.yml)
## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#dfn-delete-all-cookies)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#delete-sessionsessionidcookie)
