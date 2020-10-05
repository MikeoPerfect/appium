## Settings

Settings是appium引入的一个新概念。它们目前不是 Mobile JSON Wire 协议或 Webdriver 规范的一部分。

Settings是用来指定appium server的工作方式。

Settings有以下特点:
 - 可变性，Settings在一个会话中是可以被修改的。
 - 临时性，Settings只对当前会话生效，新建立的会话会被重置。
 - 局限性，Settings只用来控制appium server，不能用于控制被测应用或设备。

以Android的 `ignoreUnimportantViews` 为例。Android中可以设置 `ignoreUnimportantViews` 用来忽略所有与当前视图无关的元素，这样可以让用例执行的更快。注意，当用户需要访问这些被忽略的元素时，需要禁用 `ignoreUnimportantViews` 后并重新启用。

另外一个例子是Settings让appium忽略当前不可见的元素。

Settings通过下面的API实现：

### [Update Device Settings](/docs/cn/commands/session/settings/update-settings.md)

**POST** /session/:sessionId/appium/settings

>Settings使用键值对(name:value)的JSON格式，name为setting的名字，value是setting的取值。
```
{
  settings: {
   ignoreUnimportantViews : true
  }
}
```

### [Retrieve Device Settings](/docs/cn/commands/session/settings/get-settings.md)

**GET** /session/:sessionId/appium/settings

>返回当前指定 settings 的 JSON
```
{
  ignoreUnimportantViews : true
}
```

## 支持的 Settings

|名称|描述|值|
|----|----|----|
|`shouldUseCompactResponses`|查找element/elements，返回简洁(标准兼容)、快速的响应结果。默认为`true`|`false`或`true`|
|`elementResponseAttributes`|为每个元素返回逗号分隔的字段列表，仅`shouldUseCompactResponses`为`false`时生效。iOS默认值为"type，label"，Android默认值为""|例如，`"name，text，rect，attribute/name，attribute/value"`|

[图像元素](https://github.com/appium/appium/blob/master/docs/cn/advanced-concepts/image-elements.md)也有图像元素的特定settings。

### 仅 Android 支持
|名称|描述|值|
|----|----|----|
|`ignoreUnimportantViews`|设置为false时，Android设备不会忽略任何views；被设置为true时，会使用setCompressedLayoutHeirarchy()忽略标记了IMPORTANT_FOR_ACCESSIBILITY_NO或IMPORTANT_FOR_ACCESSIBILITY_AUTO（以及被系统认为不重要的）的views，从而尽量让脚本变得简单或执行的更快。默认值为`false`|`false`或`true`|

#### UiAutomator2

|名称|描述|值|
|----|----|----|
|`actionAcknowledgmentTimeout`|与[setActionAcknowledgmentTimeout](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html#setActionAcknowledgmentTimeout(long))相同。被设置为负数时将取默认值(3*1000 毫秒)。Android API 18及以上版本，由 [UiAutomator Configurator](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html) 处理。|例如，`5000`|
|`allowInvisibleElements`|控制安卓设备是否显示所有可见或不可见的元素。默认值为false|`false`或`true`|
|`enableMultiWindows`|值为true时，page source和xpath会查找所有可访问窗口，而不仅是当前的一个窗口。可以解决查找类似`android.widget.PopupWindow`窗口上的元素，默认值为`false`，只返回当前窗口。查阅 [appium-uiautomator2-server#301](https://github.com/appium/appium-uiautomator2-server/pull/301) 获取更多信息。|`true`或`false`|
|`enableNotificationListener`|控制安卓设备是否开启或关闭`NotificationListener`，默认值为`true`。|`false`或`true`|
|`keyInjectionDelay`|与:[setKeyInjectionDelay](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html#setKeyInjectionDelay(long))相同。被设置为负数时将取默认值(0 毫秒)。Android API 18及以上版本，由 [UiAutomator Configurator](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html) 处理。|例如，`5000`|
|`mjpegBilinearFiltering`|控制是否在源截图缩放算法里应用线性过滤。开启后会提升缩放后的位图质量，但可能产生[很小]的性能影响。默认值为`false`。|`false`或`true`|
|`mjpegScalingFactor`|控制截屏流的比例因子。100代表没有进行缩放（如原图大小的100%），图尺寸越大，编译时就需要消耗更多CPU性能。Int类型，取值范围为`1`到`100`，默认值为`50`|`1`到`100`|
|`mjpegServerFramerate`|控制截屏流的帧率。帧率越高，CPU负载越大，帧率最大值受限于待测设备的性能。Int类型，取值范围为`1`到`60`。默认值为`10`|`1`到`60`|
|`mjpegServerPort`|控制 MJPEG 服务端口号。Int类型，取值范围为`1024`and`65535`，默认值为`7810`。|`1024`到`65535`|
|`mjpegServerScreenshotQuality`|控制截屏流的质量。100代表质量最佳，1代表质量最差。bitmap转为JPEG格式时，值越大，编译时越需要消耗更多CPU时间。通常设置为25到90就可以，值太大特别影响性能，还不能带来可见的质量提升。值太小也会导致结果图出现明显的扭曲。Int类型，值范围为`1`and`100`，默认值为`50`|`1`到`100`|
|`normalizeTagNames`|将作为 XML tags 的所有 class names，转化为由 Apache Harmony库支持的ASCII字符的子集。Android默认使用，以避免由于 XPath 查找导致的XML解析异常。转化基于[junidecode](https://github.com/gcardone/junidecode)，需要避免 [这个问题](https://github.com/appium/appium/issues/11854)，默认值为`false`。|`false`或`true`|
|`scrollAcknowledgmentTimeout`|与:[setScrollAcknowledgmentTimeout](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html#setScrollAcknowledgmentTimeout(long))相同。被设置为负数时将取默认值(200 毫秒)。Android API 18及以上版本，由 [UiAutomator Configurator](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html) 处理。|例如`300`|
|`serverPort`|控制服务端端口号，Int类型，取值范围为`1024`and`65535`，默认值为`6790`。|`1024`到`65535`|
|`shutdownOnPowerDisconnect`|监听到电源断开[ACTION_POWER_DISCONNECTED](https://developer.android.com/reference/android/content/Intent.html#ACTION_POWER_DISCONNECTED)的系统广播后关闭服务。默认值为`true`。|`false`或`true`|
|`simpleBoundsCalculation`|值为`true`时，会计算`bounds`属性，这个方法虽然不太准确，但简单还能提升性能，Appium 1.18.0 版本开始支持，默认值为`false`|`false`或`true`|
|`trackScrollEvents`|跟踪scroll事件，值为`true`时，会把`lastScrollData`字段加到`getSession`的结果里，这样就能用于监控 scroll 进度，值为`false`时会显著提升 touch 操作的性能，默认值为`true`。|`false`或`true`|
|`waitForIdleTimeout`|与:[setWaitForIdleTimeout](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html#setWaitForIdleTimeout(long))相同。被设置为负数时将取默认值(10*1000 毫秒)。Android API 18及以上版本，由 [UiAutomator Configurator](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html) 处理。|例如`10000`|
|`waitForSelectorTimeout`|与:[setWaitForSelectorTimeout](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html#setWaitForSelectorTimeout(long))相同。被设置为负数时将取默认值(10*1000 毫秒)。Android API 18及以上版本，由 [UiAutomator Configurator](https://developer.android.com/reference/android/support/test/uiautomator/Configurator.html) 处理。|例如`10000`|
|`wakeLockTimeout`|获取唤醒锁（wake lock）超时时间。服务启动时获取并持有唤醒锁（wake lock），直到 UIAutomator2 服务被杀掉或者超时。唤醒锁（wake lock）被持有时，如果设置值为0或负数，将会立即被释放。默认值为'24*60*60*1000' 毫秒。|例如`0`，`60000`(1 min)|

### 仅 iOS 支持

#### XCUITest

|名称|描述|值|Appium支持的版本|
|----|----|----|----|
|`nativeWebTap`|启用后，可以在 Safari 里点击 non-javascript-based 页面。默认值为`false`，提醒：依赖 viewport 的大小/比例，点击元素时可能不太准确。|`true`，`false`|1.7.0+|
|`mjpegServerScreenshotQuality`|截图广播生成的截图质量，取值范围`0`to`100`。值为`0`代表压缩最多（质量最差），值为`100`代表压缩最少（质量最佳）。默认值为`25`|例如，`10`|1.10.0+|
|`mjpegServerFramerate`|值为`1..60`之间时，后台截图广播，播报截图的帧率，默认值为`10`(每秒帧数)。值设置为0时，帧率会取可达到的最大值。|例如，`60`|1.10.0+|
|`screenshotQuality`|参考[xctest/xctimagequality](https://developer.apple.com/documentation/xctest/xctimagequality?language=objc)修改手机屏幕截图的质量，默认值是`1`。参阅 [appium-xcuitest-driver](https://github.com/appium/appium-xcuitest-driver#desired-capabilities)里的`screenshotQuality`capabilities|例如`0`，`1`，`2`|1.10.0+|
|`mjpegScalingFactor`|修改截屏的比例，默认值为`100`，无缩放。Int类型，取值范围为`1`and`100`。|例如`1`，`50`，`100`|1.12.0+|
|`keyboardAutocorrection`|键盘设置里修改自动校正设置，当 WDA 基于 xctest 启动时，默认值为`false`。|`true`，`false`|1.14.0+|
|`keyboardPrediction`|键盘设置里修改预测设置，当 WDA 基于 xctest 启动时，默认值为`false`。|`true`，`false`|1.14.0+|
|`snapshotTimeout`|修改获取快照(snapshots)的过期时长。_Snapshots_主要用于生成page source，查找 XML 以及检索属性。当page source非常大，包含几百个UI元素时，需要增加 snapshotTimeout 的值。默认值为15秒。|例如`10`，`100`(秒)|1.15.0+|
|`snapshotMaxDepth`|修改遍历元素source tree的最大深度值，这个设置在获取元素source tree时有助于防止内存不足或超时，但同时也限制了source tree的深度。当在Appium log里看到这样的报错，如 _Timed out snapshotting com.apple.testmanagerd..._ message 或 _Cannot get 'xml' source of the current application_，需要考虑限制 snapshotMaxDepth 的值，因为这类问题很可能和超时有关。如果 snapshotMaxDepth 值特别小，可能会丢失元素 source tree 的部分内容。默认值为`50`|例如`100`|1.17.0+|
|`useFirstMatch`|开启这个设置后，查找单个元素速度会变快，但查找嵌套元素时会有[问题](https://github.com/appium/appium/issues/10101)。默认值是`false`|`true`，`false`|1.15.0+|
|`reduceMotion`|在辅助功能里修改减弱动态效果(motion)。|`true`，`false`|1.15.0+|
|`defaultActiveApplication`|设置当前可选程序。有助于 WebDriverAgent 从多项可选程序列表里，选择当前程序。这个设置在分屏APP自动化上很有用，默认值为`auto`，这样 WebDriverAgent 可以选择元素位于`screenPoint`的 应用，或者从当前 apps 列表里（并且列表里只有一个app）选择其中一个应用。|例如，`com.apple.Preferences`|1.15.0+|
|`activeAppDetectionPoint`|设置当前屏幕上的坐标点，如当前屏幕上有多个应用，WebDriverAgent 可以使用坐标点检测当前应用。值的格式是`x，y`，只有 x 和 y 值为float类型或者Int类型时，才是有效屏幕坐标。设置超出屏幕坐标的的值，可能会导致 WebDriverAgent 报错。默认的屏幕坐标值，分别为最小屏幕尺寸的20%，即`MIN(w，h) * 0.2，MIN(w，h) * 0.2`|例如`100，300`|1.15.0+|
|`includeNonModalElements`|iOS 13+ 设备上，是否返回所有带对话框的元素。这个设置解决了这个问题[cannot find elements on nested modal presentations](https://github.com/appium/appium/issues/13227)，但也会导致可见属性不可靠。为了提升元素可见监测，还要开启`shouldUseTestManagerForVisibilityDetection`设置(默认值是`false`)或`simpleIsVisibleCheck`capability。这个问题会在 iOS 13.0到13.2(以及 Xcode 11.0到11.2)上出现。这个查询会导致以下问题，在更新的 iOS/Xcode 版本上，includeNonModalElements 返回 nil，以及 Appium/WDA 在未使用此设置时，会返回3个相同的元素。默认值为`false`|`true`，`false`|1.15.0+|
|`acceptAlertButtonSelector`|允许自定义 accept 警告按钮 selector。这样就能处理任意元素，就像在`accept alert`命令里处理 accept 按钮那样。selector 必须是个有效的[class chain](https://github.com/facebookarchive/WebDriverAgent/wiki/Class-Chain-Queries-Construction-Rules) 表达式，查询路径必须是 alert 元素自身。如果给定的 selector 错误或者无法匹配任何元素，默认会使用按钮定位算法。|例如，<code>**/XCUIElementTypeButton[\`label CONTAINS[c] 'accept'\`]</code>|1.16.0+|
|`dismissAlertButtonSelector`|允许自定义 dismiss 警告按钮 selector。这样就能处理任意元素，就像在`dismiss alert`命令里处理 dismiss 按钮那样。selector 必须是个有效的[class chain](https://github.com/facebookarchive/WebDriverAgent/wiki/Class-Chain-Queries-Construction-Rules) 表达式，查询路径必须是 alert 元素自身。如果给定的 selector 错误或者无法匹配任何元素，默认会使用按钮定位算法。|例如，<code>**/XCUIElementTypeButton[\`label CONTAINS[c] 'dismiss'\`]</code>|1.16.0+|
|`screenshotOrientation`|在 iOS 上调整截屏方向，Appium 尝试返回截图，同时使用内部方法调整截图方向，但有时候并不生效（尤其是横屏时）。实际截屏方向受多个因素影响，如 OS 版本，model 版本，以及当前设备是真机还是模拟器。这个设置允许强制设置图片方向，默认值是`auto`|`auto`，`portrait`，`portraitUpsideDown`，`landscapeRight`，`landscapeLeft`|1.17.0+|

本文由 [nicole1010](https://github.com/nicole1010) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。