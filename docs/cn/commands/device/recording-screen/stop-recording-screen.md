# 停止屏幕录制

停止屏幕录制

## 用法示例

```java
// Java
driver.stopRecordingScreen();
driver.stopRecordingScreen(new BaseStopScreenRecordingOptions(....));
```

```python
# Python
self.driver.stop_recording_screen()
```

```javascript
// Javascript
// webdriver.io example
driver.stopRecordingScreen();

// wd example
await driver.stopRecordingScreen();
```

```ruby
# Ruby
# ruby_lib example
stop_recording_screen
stop_recording_screen remote_path: 'https://example.com', user: 'example', pass: 'pass', method: 'POST'

# ruby_lib_core example
@driver.stop_recording_screen
@driver.stop_recording_screen remote_path: 'https://example.com', user: 'example', pass: 'pass', method: 'POST'
```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.StopRecordingScreen();
```

## 支持

### Appium Server

|平台|Driver|平台版本|Appium 版本|Driver 版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/cn/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/cn/drivers/ios-uiautomation.md) | None | None | None |
| Android | [Espresso](/docs/cn/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/cn/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/cn/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/cn/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/cn/drivers/windows.md) | None | None | None |



### Appium Clients

|Language|Support|Documentation|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [static.javadoc.io](https://static.javadoc.io/io.appium/java-client/6.1.0/io/appium/java_client/screenrecording/CanRecordScreen.html#stopRecordingScreen--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.screen_record.ScreenRecord.stop_recording_screen) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L3398) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Device#stop_recording_screen-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium-dotnet-driver/blob/master/src/Appium.Net/Appium/AppiumDriver.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/appium/stop_recording_screen`


### URL 参数

|name|description|
|----|-----------|
|remotePath| 远程位置的路径, 生成的视频应该被上传到这里。 支持 http/https，ftp 这些协议。Null或空字符串值（默认设置）表示结果文件的内容应编码为Base64并作为终端响应值传递。如果生成的媒体文件太大而无法放入可用的进程内存中，将引发异常。这个选项仅在屏幕录制进行中将 `forceRestart` 不设置为 `true` 时有效。|
|username| 用于远程身份验证的用户的名称 |
|password| 用于远程身份验证的用户的密码 |
|method|http multipart upload 方法名。默认使用 `PUT` 方法。|


### JSON 参数

Null


### 响应

Base64 编码字符串。如果设置了 `remote_path`，将会响应一个空的字符串。 (`string`)


## 参考

* [JSONWP 规范](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L373)
