# 获取所有Context

获取所有可以自动化的context

## 使用示例

```java
// Java
Set<String> contextNames = driver.getContextHandles();

```

```python
# Python
contexts = driver.contexts

```

```javascript
// Javascript
// webdriver.io example
let contexts = driver.getContexts();

// wd example
let contexts = await driver.contexts();

```

```ruby
# Ruby
# ruby_lib example
context = available_contexts

# ruby_lib_core example
context = @driver.available_contexts

```

```php
# PHP
$contexts = $driver->contexts();

```

```csharp
// C#
List<string> AllContexts = new List<string>();
     foreach (var context in (driver.Contexts))
     {
         AllContexts.Add(context);
     }

```

## 描述


获取所有的context. 它至少包含native context. 也可能有零个或者多个的webview context. 关于context的名称格式信息, 可点击[获取当前上下文](/docs/cn/commands/context/get-context.md).
在iOS上, 使用XCUITest driver的时候, 可以用 `mobile: getContexts` [mobile command](/docs/cn/commands/mobile-command.md) 去替代标准方法，以便获取到每个context的标题与url.
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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/AppiumDriver.html#getContextHandles--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.context.Context.contexts) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/doc/api.md) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Device#available_contexts-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 路径

`GET /session/:session_id/contexts`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|新建会话(session)后用来标识当前会话(session)的ID|


### JSON 参数

无


### 响应

返回一个数组，包含了所有可用的context (`Array<String>`)


## 参考

* [JSONWP 规范](https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md#webviews-and-other-contexts)
