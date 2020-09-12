# 开始屏幕录制

开始屏幕录制

## 用法示例

```java
// Java
driver.startRecordingScreen();
driver.startRecordingScreen(new BaseStartScreenRecordingOptions(....));
```

```python
# Python
self.driver.start_recording_screen()
```

```javascript
// Javascript
// webdriver.io example
driver.startRecordingScreen();

// wd example
await driver.startRecordingScreen();
```

```ruby
# Ruby
# ruby_lib example
start_recording_screen
start_recording_screen video_size: '1280x720', time_limit: '180', bit_rate: '5000000' # Android
start_recording_screen video_type: 'h264', time_limit: '260' # iOS

# ruby_lib_core example
@driver.start_recording_screen
@driver.start_recording_screen video_size: '1280x720', time_limit: '180', bit_rate: '5000000' # Android
@driver.start_recording_screen video_type: 'h264', time_limit: '260' # iOS
```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.StartRecordingScreen(
    AndroidStartScreenRecordingOptions.GetAndroidStartScreenRecordingOptions()
        .WithTimeLimit(TimeSpan.FromSeconds(10))
        .WithBitRate(500000)
        .WithVideoSize("720x1280"));
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

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [static.javadoc.io](https://static.javadoc.io/io.appium/java-client/6.1.0/io/appium/java_client/screenrecording/CanRecordScreen.html#startRecordingScreen-T-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.screen_record.ScreenRecord.start_recording_screen) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L3412) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [Android](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Android/Device#start_recording_screen-instance_method) [iOS](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Ios/Xcuitest/Device#start_recording_screen-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API 规范


### 终端

`POST /session/:session_id/appium/start_recording_screen`

### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）ID|

### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| options | `object` | The following parameters of the action |
| options.remotePath | `string` | 远程位置的路径, 生成的视频应该被上传到这里。支持 http/https，ftp 协议。Null或空字符串值（默认）表示结果文件的内容使用 Base64 编码并作为响应值传递给终端。如果生成的媒体文件太大而无法放入进程可用内存中，将引发异常。这个选项仅在屏幕录制进行中 `forceRestart` 不为 `true` 时有效。 |
| options.username | `string` | 用于远程身份验证的用户的名称 |
| options.password | `string` | 用于远程身份验证的用户的密码 |
| options.method | `string` | http multipart upload 方法名。默认使用 `PUT` 方法。 |
| options.forceRestart | `boolean` | 是尝试捕获并上载/返回当前正在运行的屏幕录制（服务器上默认为 `false`），还是忽略它的结果并立即开始新的录制（`true`）。 |
| options.timeLimit | `string` | 录制时间。默认录制180秒。 |
| options.videoType | `string` | (iOS Only)要屏幕录制的视频格式。 可用的格式是 `ffmpeg -codecs` 的输出，例如 `libx264` 和 `mpeg4`。默认使用 `mpeg4` 格式。 |
| options.videoQuality | `string` | (iOS Only) 视频录制的画质 (低, 中, 高, 原画 - 默认使用中画质). |
| options.videoFps | `string` | (iOS Only) 每秒录制视频的帧数。如果生成的视频太慢或太快，请更改此值。默认为10。这可以减小生成的文件大小。|
| options.videoScale | `string` | (iOS Only) 缩放比例。查看 https://trac.ffmpeg.org/wiki/Scaling 获得可用比例。例如 720p 的默认比例为“1280:720”。这可以减小或增加生成的文件大小。默认情况下不应用缩放。 |
| options.bitRate | `string` | (Android Only) 视频的比特率，单位为Mbps。Android API 低于 27 的，默认为 4mbp/s（4000000）。API 27 及以上的为 20 Mb/s（20000000）。|
| options.videoSize | `string` | (Android Only) 格式为widthxheight。默认为设备的本机显示分辨率（如果支持），如果不支持，则为 1280x720。为了获得最佳效果，请使用设备的高级视频编码（AVC）编码器支持的大小。例如，“1280x720” |
| options.bugReport | `string` | (Android Only) 将其设置为 `true`，以便在视频覆盖上显示其他信息，例如时间戳，这对捕获视频以说明错误很有帮助。此选项仅在 API 27（Android O）之后才受支持. |

### 响应

null

## 参考

* [JSONWP 规范](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L370)
