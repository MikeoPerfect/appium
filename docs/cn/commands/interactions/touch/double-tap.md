# Double Tap

手指在触摸屏上双击事件

## 使用样例

```java
// Java
TouchActions action = new TouchActions(driver);
action.doubleTap(element);
action.perform();

```

```python
# Python
from appium.webdriver.common.touch_action import TouchAction
# ...
actions = TouchAction(driver)
actions.double_tap(element)
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.touchDoubleClick(element.elementId);
// wd example
// Using tapElement method
await driver.tapElement(elementOne);

// Using touch actions
let action = new wd.TouchAction();
action.tap({el: element});
await action.perform();

```

```ruby
# Ruby
# ruby_lib example
touch_action.double_tap(element).perform

# ruby_lib_core example
@driver.touch_action.double_tap(element).perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
TouchActions action = new TouchActions(driver);
action.DoubleTap(element);
action.Perform();

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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/touch/TouchActions.html#doubleTap-org.openqa.selenium.WebElement-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/py/webdriver/selenium.webdriver.common.touch_actions.html#selenium.webdriver.common.touch_actions.TouchActions.double_tap) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L425) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium%2FWebDriver%2FTouchActionBuilder:double_tap) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Interactions/TouchActions.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/touch/doubleclick`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| element | `number` | 双击的元素ID |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidtouchdoubleclick)
