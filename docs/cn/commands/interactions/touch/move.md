
# Move To

手指在屏幕上移动

## 使用样例

```java
// Java
TouchActions action = new TouchActions(driver);
action.down(10, 10);
action.moveTo(50, 50);
action.perform();

```

```python
# Python
from appium.webdriver.common.touch_action import TouchAction
# ...
actions = TouchAction(driver)
actions.tap_and_hold(element)
actions.move_to(element, 50, 50)
actions.perform()

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
let action = new wd.TouchAction(driver);
action.press({x: 10, y: 10})
      .wait(1000)
      .moveTo({x: 50, y: 50})
      .release();
await action.perform();

```

```ruby
# Ruby
# ruby_lib example
touch_action.down(element).move_to().perform

# ruby_lib_core example
@driver.touch_action.down(element).move_to().perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
TouchActions action = new TouchActions(driver);
action.Down(10, 10);
action.Move(50, 50);
action.Perform();

```


## 描述

As of Appium 1.8.0 all move actions take coordinates that are absolute.



## 支持


### Appium Server

|Platform|Driver|Platform Versions|Appium Version|Driver Version|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |



### Appium 客户端

|语言| 支持 |文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/touch/TouchActions.html#down-int-int-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/py/webdriver/selenium.webdriver.common.touch_actions.html#selenium.webdriver.common.touch_actions.TouchActions.move) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1531) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium%2FWebDriver%2FTouchActionBuilder:move) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Interactions/TouchActions.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/touch/move`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| x | `number` | 屏幕上的X坐标 |
| y | `number` | 屏幕上的Y坐标 |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidtouchmove)
