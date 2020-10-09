
# 拨打电话

拨打电话 (只支持模拟器)

## 使用示例

```java
// Java
driver.makeGsmCall("5551234567", GsmCallActions.CALL);

```

```python
# Python
self.driver.make_gsm_call('5551234567', GsmCallActions.CALL)

```

```javascript
// Javascript
// webdriver.io example
driver.gsmCall('555-123-4567', 'call');

// wd example
await driver.gsmCall('555-123-4567', 'Phone');

```

```ruby
# Ruby
# ruby_lib example
gsm_call(phone_number: '5551234567', action: :call)

# ruby_lib_core example
@driver.gsm_call(phone_number: '5551234567', action: :call)

```

```php
# PHP
// TODO

```

```csharp
// C#
// TODO

```


## 支持

### Appium 服务端

|Platform|Driver|Platform Versions|Appium Version|Driver Version|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/cn/drivers/ios-xcuitest.md) | None | None | None |
|  | [UIAutomation](/docs/cn/drivers/ios-uiautomation.md) | None | None | None |
| Android | [UiAutomator2](/docs/cn/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [Espresso](/docs/cn/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator](/docs/cn/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/cn/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/cn/drivers/windows.md) | None | None | None |



### Appium 客户端

|Language|Support|Documentation|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/android/SupportsSpecialEmulatorCommands.html#makeGsmCall-java.lang.String-io.appium.java_client.android.GsmCallActions-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.android.html#webdriver.extensions.android.gsm.Gsm.make_gsm_call) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L3183) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/master/Appium/Core/Android/Device/Emulator#gsm_call-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 路径

`POST /session/:session_id/appium/device/gsm_call`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|新建会话(session)后用来标识当前会话(session)的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| phoneNumber | `string` | 拨打者的手机号码 |
| action | `string` | action的值如下 - 'call', 'accept', 'cancel', 'hold'. |


### 响应

null


## 参考

* [JSONWP 规范](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L394)
