
# Button Up

释放之前按住的鼠标按钮

## 使用样例

```java
// Java
Actions action = new Actions(driver);
action.moveTo(element);
action.clickAndHold();
action.moveTo(element, 10, 10);
action.release();
action.perform();

```

```python
# Python
actions = ActionChains(driver)
actions.move_to_element(element)
actions.click_and_hold()
actions.move_to_element(element, 10, 10)
action.release();
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.moveTo(element);
driver.buttonDown();
driver.moveTo(element, 10, 10);
driver.buttonUp();

// wd example
await driver.moveTo(element);
await driver.buttonDown();
await driver.moveTo(element, 10, 10);
await driver.buttonUp();

```

```ruby
# Ruby
# ruby_lib example
action.click_and_hold(el).move_to(el, 10, 10).release.perform

# ruby_lib_core example
@driver.action.click_and_hold(el).move_to(el, 10, 10).release.perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
Actions action = new Actions(driver);
action.MoveToElement(element);
action.ClickAndHold();
action.MoveToElement(element, 10, 10);
action.Release();
action.Perform();

```


## 描述

对于每个发出的buttondown命令必须调用一次buttonup命令。 请参阅click和 buttondown事件的注释，以了解乱序命令的含义



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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/Actions.html#clickAndHold--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.common.action_chains.ActionChains.release) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1645) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/ActionBuilder:release) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Interactions/Actions.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/buttonup`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| button | `number` | 按钮参数值，{LEFT = 0，MIDDLE = 1，RIGHT = 2}； 如果未指定，默认为鼠标左键 |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidbuttonup)
