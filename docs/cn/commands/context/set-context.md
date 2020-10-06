# 设置当前Context

设置Context

## 使用示例

```java
// Java
Set<String> contextNames = driver.getContextHandles();
driver.context(contextNames.toArray()[1]);
// ...
driver.context("NATIVE_APP");

```

```python
# Python
webview = driver.contexts[1]
driver.switch_to.context(webview)
# ...
driver.switch_to.context('NATIVE_APP')

```

```javascript
// Javascript
// webdriver.io example
let contexts = driver.getContexts();
driver.switchContext(contexts[1]);
// ...
driver.switchContext('NATIVE_APP');

// wd example
let contexts = await driver.contexts();
await driver.context(contexts[1]);
// ...
await driver.context('NATIVE_APP');

```

```ruby
# Ruby
# ruby_lib example
webview = available_contexts[1]
set_context(webview)
# ...
set_context('NATIVE_APP')

# ruby_lib_core example
webview = @driver.available_contexts[1]
@driver.set_context(webview)
# ...
@driver.set_context('NATIVE_APP')

```

```php
# PHP
$contexts = $driver->contexts();
$driver->context($contexts[1]);
// ...
$driver->context('NATIVE_APP');

```

```csharp
// C#
// Switch to specific webview
  List<string> AllContexts = new List<string>();
    foreach (var context in (driver.Contexts))
    {
        AllContexts.Add(context);
    }
  driver.Context = (AllContexts[1]);
 // Switch to NATIVE_APP
 driver.Context = ("NATIVE_APP");

```

## 描述

通过传入的context来设置当前的context，如果是设置webview为当前的context，则将尝试与web view进行连接:
  
  * iOS - 通过远程调试(remote debugger)与web view进行连接
  * Android - 启动[Chromedriver](/docs/cn/writing-running-appium/web/chromedriver.md)
    进程去创建一个会话(session)与web view进行连接


想了解contexts的相关信息，可点击查看Appium的[自动化混合应用](/docs/cn/writing-running-appium/web/hybrid.md).


## 支持


### Appium 服务端

|Platform|Driver|Platform Versions|Appium Version|Driver Version|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | None | None | None |



### Appium 客户端

|Language|Support|Documentation|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/AppiumDriver.html#context-java.lang.String-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.context.Context.context) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/doc/api.md) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Device#set_context-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 路径

`POST /session/:session_id/context`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|新建会话(session)后用来标识当前会话(session)的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| name | `String` | 要设置的context的名称 |


### 响应

null

## 参考

* [JSONWP 规范](https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md#webviews-and-other-contexts)
