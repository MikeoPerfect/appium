
# Flick

手指在触摸屏上滑动的动作事件

## 使用样例

```java
// Java
TouchActions action = new TouchActions(driver);
action.flick(element, 1, 10, 10);
action.perform();

```

```python
# Python
from appium.webdriver.common.touch_action import TouchAction
# ...
actions = TouchAction(driver)
actions.flick_element(element, 1, 10, 10)
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.touchFlick(10, 10, element, 1);

// wd example
await element.flick(1, 10, 10);

```

```ruby
# Ruby
# ruby_lib example
touch_action.flick(element, 1, 10, 10).perform

# ruby_lib_core example
@driver.touch_action.flick(element, 1, 10, 10).perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
TouchActions action = new TouchActions(driver);
action.Flick(element, 10, 10, 1);
action.Perform();

```



## 支持


### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | None | None | None |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |



### Appium 客户端

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/touch/TouchActions.html#flick-org.openqa.selenium.WebElement-int-int-int-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/py/webdriver/selenium.webdriver.common.touch_actions.html#selenium.webdriver.common.touch_actions.TouchActions.flick_element) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1513) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium%2FWebDriver%2FTouchActionBuilder:flick) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Interactions/TouchActions.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/touch/flick`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| element | `string` | 滑动开始的元素的ID |
| xoffset | `number` | 以像素为单位的x方向的偏移量 |
| yoffset | `number` | 以像素为单位的y方向的偏移量 |
| speed | `number` | 速度，单位为“像素/秒” |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidtouchflick)
