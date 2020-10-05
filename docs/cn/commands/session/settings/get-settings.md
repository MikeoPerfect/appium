# 提取设备的设置项

提取设备的当前设置项

## 使用样例

```java
// Java
Map<String, Object> settings = driver.getSettings();

```

```python
# Python
self.driver.get_settings

```

```javascript
// Javascript
// webdriver.io example
let settings = driver.getSettings();

// wd example
await driver.settings();

```

```ruby
# Ruby
# ruby_lib example
get_settings

# ruby_lib_core example
@driver.get_settings

```

```php
// Not supported
```

```csharp
// Not supported
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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/HasSettings.html#getSettings--) |
|[Python](https://github.com/appium/python-client/releases/latest)| None | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.settings.Settings.get_settings) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L3018) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| None | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Device#get_settings-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None |  |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None |  |


## HTTP API 规范


### 终端

`GET /session/:session_id/appium/settings`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

None


### 响应

所有当前指定设置的JSON对象, 参考[Settings API](/docs/en/advanced-concepts/settings.md). (`array<object>`)


## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L587)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 2b60bef0264515c912137d038c8f64e580050497, 11 May 2020