# 获取性能数据类型

返回支持读取的系统状态信息类型，例如cpu，内存，网络流量和电池信息
## 使用样例

```java
// Java
List<String> performanceTypes = driver.getSupportedPerformanceDataTypes();

```

```python
# Python
self.driver.get_performance_data_types()

```

```javascript
// Javascript
// webdriver.io example
driver.getPerformanceDataTypes();

// wd example
await driver.getSupportedPerformanceDataTypes();

```

```ruby
# Ruby
# ruby_lib example
get_performance_data_types

# ruby_lib_core example
@driver.get_performance_data_types

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
// Not supported

```


## 支持

### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | None | None | None |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | None | None | None |


### Appium Clients

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/android/HasSupportedPerformanceDataType.html#getSupportedPerformanceDataTypes--) |
|[Python](https://github.com/appium/python-client/releases/latest)| None | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.android.html#webdriver.extensions.android.performance.Performance.get_performance_data_types) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L3398) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Android/Device#get_performance_data_types-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API 规范

### 终端

`POST /session/:session_id/appium/performanceData/types`

### URL 参数

|名称|描述|
|----|-----------|
|session_id|将命令路由到服务器的sessionID|

### JSON 参数

None

### 响应

可用的性能数据类型 (cpuinfo | batteryinfo | networkinfo | memoryinfo) (`array<string>`)

## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L376)
