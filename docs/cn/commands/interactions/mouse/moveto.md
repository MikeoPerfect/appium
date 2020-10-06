
# Move Mouse To

将鼠标移动指定元素的偏移量

## 使用样例

```java
// Java
Actions action = new Actions(driver);
action.moveTo(element, 10, 10);
action.perform();

```

```python
# Python
actions = ActionChains(driver)
actions.move_to(element, 10, 10)
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
$(element).moveTo(10, 10);

// wd example
await driver.moveTo(element, 10, 10);

```

```ruby
# Ruby
# ruby_lib example
mouse.move_to(element)
mouse.move_to(element, 5, 5)

# ruby_lib_core example
@driver.mouse.move_to(element)
@driver.mouse.move_to(element, 5, 5)

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
Actions action = new Actions(driver);
action.MoveToElement(element, 10, 10);
action.Perform();

```


## 描述

如果未指定任何元素，则移动是相对于当前鼠标光标的。 如果提供了元素但没有偏移，则鼠标将移动到元素的中心。 如果该元素不可见，则将其滚动到视图中。



## 支持


### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | None | None | None |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | None | None | None |
|  | [Espresso](/docs/en/drivers/android-espresso.md) | None | None | None |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | None | None | None |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |



### Appium 客户端

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/Actions.html#moveToElement-org.openqa.selenium.WebElement-) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.common.action_chains.ActionChains.move_to_element) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1600) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Mouse:move_to) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/moveto`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| element | `string` | 要移动到的元素的ID。 如果未指定，就是相对于鼠标位置 |
| xoffset | `number` | 相对于元素左上角的X方向的偏移量。 如果未指定，则鼠标将移动到元素的中间 |
| yoffset | `number` | 相对于元素左上角的Y方向的偏移量。 如果未指定，则鼠标将移动到元素的中间 |


### 响应

null


## 支持

* [W3C Specification](https://drafts.csswg.org/cssom-view/#dom-window-moveto)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#post-sessionsessionidmoveto)
