
# Multi Touch Perform

执行多点触控动作序列

## 使用样例

```java
// Java
TouchActions actionOne = new TouchAction();
actionOne.press(10, 10);
actionOne.moveTo(10, 100);
actionOne.release();
TouchActions actionTwo = new TouchAction();
actionTwo.press(20, 20);
actionTwo.moveTo(20, 200);
actionTwo.release();
MultiTouchAction action = new MultiTouchAction();
action.add(actionOne);
action.add(actionTwo);
action.perform();

```

```python
# Python
from appium.webdriver.common.touch_action import TouchAction
from appium.webdriver.common.multi_action import MultiAction
# ...
a1 = TouchAction()
a1.press(10, 20)
a1.move_to(10, 200)
a1.release()

a2 = TouchAction()
a2.press(10, 10)
a2.move_to(10, 100)
a2.release()

ma = MultiAction(self.driver)
ma.add(a1, a2)
ma.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.multiTouchPerform([
  { action: 'press', options: { x: 100, y: 250 }},
  { action: 'moveTo', options: { x: 300, y: 100 }},
  { action: 'release' }
]);

// wd example
let action = new wd.MultiTouchAction();
action.press({x: 10, y: 10});
action.moveTo({x: 10, y: 100});
action.release();
await action.perform();

```

```ruby
# Ruby
# ruby_lib example
multi_touch.down(element).move_to(10, 100).up(50, 50).perform

# ruby_lib_core example
@driver.multi_touch.down(element).move_to(10, 100).up(50, 50).perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
// TODO C# sample

```



## 支持


### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [appium.github.io](https://appium.github.io/java-client/io/appium/java_client/MultiTouchAction.html) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.common.html#module-webdriver.common.multi_action) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1546) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/github/appium/ruby_lib/Appium/MultiTouch) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/touch/multi/perform`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| action | `string` | 需要执行的操作类型（moveTo\|release\|press\|tap\|wait） |
| options | `object` | 动作操作参数 |
| opts.element | `string` | 元素的ID |
| opts.x | `number` | 操作的X坐标（相对于左上角） |
| opts.y | `number` | 操作的X坐标（相对于左上角） |
| opts.count | `number` | Tap次数 |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L348)
