
# Button Down

单机当前鼠标坐标处，并按住鼠标左键

## 使用样例

```java
// Java
Actions action = new Actions(driver);
action.moveTo(element);
action.clickAndHold();
action.perform();

```

```python
# Python
actions = ActionChains(driver)
actions.move_to_element(element)
actions.click_and_hold()
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
driver.moveTo(element);
driver.buttonDown();

// wd example
await driver.moveTo(element);
await driver.buttonDown();

```

```ruby
# Ruby
# ruby_lib example
action.move_to(element).click_and_hold.perform

# ruby_lib_core example
@driver.action.move_to(element).click_and_hold.perform

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
action.Perform();

```


## 描述

请注意，下一个与鼠标相关的命令应该是buttonup。 任何其他鼠标命令（例如单击或其他对buttondown的调用）将产生未定义的行为



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



### Appium客户端

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/Actions.html#clickAndHold--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.common.action_chains.ActionChains.click_and_hold) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1625) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/ActionBuilder:click_and_hold) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/SeleniumHQ/selenium/blob/master/dotnet/src/webdriver/Interactions/Actions.cs) |


## HTTP API 规范


### 终端

`POST /session/:session_id/buttondown`


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

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidbuttondown)
