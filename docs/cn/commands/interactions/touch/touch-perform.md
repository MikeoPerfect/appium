
# Touch Perform

执行触摸动作序列

## 使用样例

```java
// Java
TouchAction action = new TouchAction(driver);
action.press(10, 10);
action.moveTo(10, 100);
action.release();
action.perform();

```

```python
# Python
from appium.webdriver.common.touch_action import TouchAction
// ...
actions = TouchAction(driver)
actions.tap_and_hold(20, 20)
actions.move_to(10, 100)
actions.release()
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.touchPerform([
  { action: 'press', options: { x: 100, y: 250 }},
  { action: 'moveTo', options: { x: 300, y: 100 }},
  { action: 'release' }
]);

// wd example
let action = new wd.TouchAction();
action.press({x: 10, y: 10});
action.moveTo({x: 10, y: 100});
action.release();
await action.perform();

```

```ruby
# Ruby
# ruby_lib example
touch_action.down(element).move_to(10, 100).up(50, 50).perform

# ruby_lib_core example
@driver.touch_action.down(element).move_to(10, 100).up(50, 50).perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
TouchAction action = new TouchAction(driver);
action.Press(10, 10);
action.MoveTo(10, 100);
action.Release();
action.Perform();

```


## 描述

此功能仅在本地环境中可用

“Touch-Perform”的工作原理与其他单一的触摸交互类似，不同之处在于它允许你将多个触摸操作合并成一个命令。这很有用，因为Appium命令是通过网络发送的，而且命令之间存在延迟。这种延时会使一些特定的触摸交互无法实现其功能，因为某些命令交互是需要按照顺序进行的。例如，对于垂直方向需要按压屏幕，然后向下移动到y坐标，然后释放。 为了使其正常工作，交互之间不能有延迟。 



## 支持


### Appium Server

|平台|Driver|平台版本|Appium 版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |



### Appium 客户端

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/TouchAction.html) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.common.html#module-webdriver.common.touch_action) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1546) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib/Appium/TouchAction) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/blob/master/src/Appium.Net/Appium/MultiAction/TouchAction.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/touch/perform`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| action | `string` | 需要执行的动作类型 (moveTo\|release\|press\|tap\|wait) |
| options | `object` | 动作参数 |
| opts.element | `string` | 元素的ID |
| opts.x | `number` | 操作的X坐标（相对于左上角） |
| opts.y | `number` | 操作的Y坐标（相对于左上角） |
| opts.count | `number` | Tap次数 |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L345)
