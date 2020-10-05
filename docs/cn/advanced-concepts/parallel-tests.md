## Android 并发测试

Appium 给用户提供了在单机上启动多个 Android sessions 的方案。可以使用任意可用端口启动 Appium 服务。

注意，在*同一设备上*不能运行多个 session

以下是启动多个 Android sessions 的一些重要参数：

- `udid` 设备id
- `chromedriverPort` chromedriver 端口(如果使用 webviews or chrome)
- `mjpegServerPort` 如果使用 [appium-uiautomator2-driver](https://github.com/appium/appium-uiautomator2-driver)，需要为每个并发 session 设置一个唯一的 MJPEG 服务端口，否则可能会有端口冲突问题，如[这个问题](https://github.com/appium/appium/issues/7745)。
- `systemPort` 如果使用 [appium-uiautomator2-driver](https://github.com/appium/appium-uiautomator2-driver)，需要为每个并发 session 设置一个唯一的系统端口，否则可能会有端口冲突问题，如[这个问题](https://github.com/appium/appium/issues/7745)。

### iOS 并发测试

Xcode9 以来，Appium 支持在真机和模拟器上进行并发测试。可以使用任意可用端口启动 Appium 服务。

以下是在 iOS 上启动多个 session 的重要参数：

#### 真机

- `udid` 每个并发 session 必须设置唯一的设备UDID。
- `wdaLocalPort` 每个并发 session 必须设置唯一的端口号，默认的端口号是8100。
- `derivedDataPath` 需要为每个 driver 实例设置唯一的导出数据根路径，这样有助于避免冲突，以及加快并发执行速度。

#### 模拟器

- 为每个并发 session 设置唯一的模拟器 UDID 或者一组唯一的 `deviceName` 和 `platformVersion`。`udid`，模拟器 UDID(可以从 xcrun simctl list 中获取)，`deviceName` 和 `platformVersion`，可以定位到对应设备名和平台版本号的模拟器。
- `wdaLocalPort` 每个并发 session 必须设置唯一的端口号，默认的端口号是8100。
- `derivedDataPath` 需要为每个 driver 实例设置唯一的导出数据根路径，这样有助于避免冲突，以及加快并发执行速度。

### 故障排查

在 Jenkins 上运行时，当在相同机器上运行多个并发测试 jobs 时， 需要注意[ProcessTreeKiller](https://wiki.jenkins.io/display/JENKINS/ProcessTreeKiller)。
如果在一个测试 job 里使用大量模拟器，当第一个测试结束，Jenkins 可能会 kill 掉所有模拟器，这会导致剩下的测试 jobs 报错！

使用 `BUILD_ID=dontKillMe` 来防止这个问题发生。

本文由 [nicole1010](https://github.com/nicole1010) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。