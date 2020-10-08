
# Click单击

在当前鼠标坐标处单击任意鼠标按钮

## 使用样例

```java
// Java
Actions action = new Actions(driver);
action.moveTo(element);
action.click();
action.perform();

```

```python
# Python
actions = ActionChains(driver)
actions.move_to_element(element)
actions.click()
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
$("~SomeId").click();

// wd example
await driver.moveTo(element);
await driver.click();

```

```ruby
# Ruby
# ruby_lib example
action.move_to(element).click.perform

# ruby_lib_core example
@driver.action.move_to(element).click.perform

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
Actions action = new Actions(driver);
action.MoveToElement(element);
action.Click();
action.Perform();

```



## 支持


### Appium Server

|平台|Driver| 平台版本 |Appium版本|Driver版本|
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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/Actions.html#click--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.common.action_chains.ActionChains.click) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1665) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Mouse:click) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/click`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON Parameters

|name|type|description|
|----|----|-----------|
| button | `number` | 按钮参数值，{LEFT = 0，MIDDLE = 1，RIGHT = 2}； 如果未指定，默认为鼠标左键 |


### 响应

null


## 支持

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidclick)
