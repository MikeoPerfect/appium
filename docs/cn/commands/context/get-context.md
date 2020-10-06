# 获取当前Context

获取Appium运行时的当前Context

## 使用示例

```java
// Java
String context = driver.getContext();

```

```python
# Python
context = driver.current_context
# or
context = driver.context

```

```javascript
// Javascript
// webdriver.io example
let context = driver.getContext();

// wd example
let context = await driver.currentContext();

```

```ruby
# Ruby
# ruby_lib example
context = current_context

# ruby_lib_core example
context = @driver.current_context
```

```php
# PHP
$context = $driver->context();

```

```csharp
// C#
string Context = driver.Context;

```


## 描述

查找目前的context. 它有可能是原生的context: `NATIVE_APP` ，也可能是webview的context:
  * iOS - `WEBVIEW_<id>`
  * Android - `WEBVIEW_<package name>`

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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/AppiumDriver.html#getContext--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.context.Context.current_context) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/doc/api.md) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Device#current_context-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API 规范


### 路径

`GET /session/:session_id/context`


### URL参数

|名称|描述|
|----|-----------|
|session_id|新建会话(session)后用来标识当前会话(session)的ID|


### JSON参数

无

### 响应

当前context的名称(`String`)


## 参考

* [JSONWP 规范](https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md#webviews-and-other-contexts)
