## tvOS 支持

- 通过 XCUITest 驱动，Appium 1.13.0+ 支持 tvOS 自动化。
    - 在 Apple TV 4K 上不支持。因为 [ios-deploy](https://github.com/ios-control/ios-deploy) 不支持无线设备。

<img src="https://user-images.githubusercontent.com/5511591/55161297-876e0200-51a8-11e9-8313-8d9f15a0db9d.gif" width=50%>

## 设置

通过修改`platformName`参数，你可以在tvOS上运行测试。

```json
{
    "automationName": "XCUITest",
    "platformName": "tvOS", // here
    "platformVersion": "12.2",
    "deviceName": "Apple TV",
    ...
}
```

小贴士：编译 WDA 支持 tvOS
- 更新到最新版本的 Carthage
- 确保机器上有 tvOS 模拟器
    - 比如：运行`xcrun simctl list | grep "com.apple.CoreSimulator.SimRuntime.tvOS"`看看结果。
    - 如果没有tvOS模拟器，新版本的 Carthage 会抛出这样的错误： `Could not find any available simulators for tvOS`

## 限制
tvOS上不支持手势动作，某些命令也不支持，比如`pasteboard`。

我们可以简单地按`up/down/left/right/home`来聚焦（focus）元素。tvOS 在_focused_的元素上执行动作。你可以通过[Attributes API](http://appium.io/docs/cn/commands/element/attributes/attribute/)得到`focus`的元素。_Get active element_ API 会返回聚焦的元素。


## 基础动作

_pressButton_ 和 _get active element_ 是 tvOS 上的基础动作。由于 tvOS 也有动画，所以需要考虑使用 `wait` 方法。

```ruby
# Ruby
element = @driver.find_element :accessibility_id, 'element on the app'
# Returns true if the element is focused, otherwise false
element.focused #=> 'true'
# Appium moves the focus to the element by pressing the corresponding keys and clicking the element
element.click
# Get the app state
@driver.app_state('test.package.name') # => :running_in_foreground
# Press keys
@driver.execute_script 'mobile: pressButton', { name: 'Home' }
# Move focus and get the focused element
@driver.execute_script 'mobile: pressButton', { name: 'Up' }
# Get a focused element
element = @driver.switch_to.active_element
element.label #=> "Settings"
```

```Python
# Python
element = driver.find_element_by_accessibility_id('element on the app')
element.get_attribute('focused')
element.click()
driver.query_app_state('test.package.name')
driver.execute_script('mobile: pressButton', { 'name': 'Home' })
driver.execute_script('mobile: pressButton', { 'name': 'Up' })
element = driver.switch_to.active_element
element.get_attribute('label')
```

```java
// Java
WebElement element = driver.findElementByAccessibilityId("element on the app");
element.getAttribute("focused");
element.click();
driver.queryAppState("test.package.name");
driver.executeScript("mobile: pressButton", ImmutableMap.of("name", "Home"));
driver.executeScript("mobile: pressButton", ImmutableMap.of("name", "Up"));
element = driver.switchTo().activeElement();
element.getAttribute("label");
```

```javascript
// webdriver.io example
const element = $('~SomeAccessibilityId');
element.getAttribute('focused');
element.click();
driver.execute('mobile: pressButton', {name: 'Home'});
driver.execute('mobile: pressButton', {name: 'Up'});
const activeElement = driver.getActiveElement();
activeElement.getAttribute('label');

// WD example
const element = await driver.elementByAccessibilityId('element on the app');
await element.getAttribute('focused');
await element.click();
await driver.execute('mobile: pressButton', {name: 'Home'});
await driver.execute('mobile: pressButton', {name: 'Up'});
const activeElement = await driver.active();
await activeElement.getAttribute('label');
```

## 更多动作
tvOS 提供基于 [remote controller](https://developer.apple.com/design/human-interface-guidelines/tvos/remote-and-controllers/remote/) 的动作。Appium 通过`mobile: pressButton`提供了 _Buttons_ 等一些列动作，包括 `menu`，`up/down/left/right`，`home`，`playpause` 和 `select`。如果你发送不支持的 button 名字给服务器，在错误信息中会罗列支持的动作。

 如果提供了 `find element/s` 和 `click`操作 ，Appium 会自动计算 `up/down/left/right` 和 `select` 顺序。你不需要每次都关心哪个按钮被点击了。
 你也可以设置一个焦点或者开始/暂停播放。在 tvOS 中，`menu`按钮作为返回键。

## 测试运行环境
- 使用模拟器或者真机
- 在支持[HeadSpin](https://headspin.io)的真机上测试或者开发

## 资源
- 相关问题:
    - https://github.com/appium/appium/pull/12401
    - 比如 [appium-xcuitest-driver#911](https://github.com/appium/appium-xcuitest-driver/pull/911), [appium-xcuitest-driver#939](https://github.com/appium/appium-xcuitest-driver/pull/939), [appium-xcuitest-driver#931](https://github.com/appium/appium-xcuitest-driver/pull/931), [appium/WebDriverAgent/pull/163](https://github.com/appium/WebDriverAgent#163)
