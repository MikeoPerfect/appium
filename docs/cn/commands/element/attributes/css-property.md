# 获取CSS元素的值

查询web元素CSS属性的值

## 样例

```java
// Java
MobileElement element = (MobileElement) driver.findElementById("SomeId");
String cssProperty = element.getCssValue("style");

```

```python
# Python
cssProperty = self.driver.find_element_by_accessibility_id('SomeId').value_of_css_property("style")

```

```javascript
// Javascript
// webdriver.io example
let cssProperty = $("~SomeId").getCSSProperty("style");

// wd example
let element = await driver.elementById("SomeId");
let cssProperty = await element.getComputedCss();

```

```ruby
# Ruby
# ruby_lib example
find_element(:id, 'SomeId').css_value

# ruby_lib_core example
@driver.find_element(:id, 'SomeId').css_value

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
var element = driver.FindElementById("SomeId");
string cssProperty = element.GetCssValue("style");

```

## 描述

要查询的CSS属性应该使用CSS属性名指定，而不是JavaScript属性名（例如background-color而不是backgroundColor）。
此命令仅适用于webview上下文

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

### Appium Clients

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html#getCssValue--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webelement.WebElement.value_of_css_property) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1447) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Element:css_value) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/blob/master/src/Appium.Net/Appium/AppiumWebElement.cs) |

## HTTP API规范
### 端点

### URL参数
|名称|描述|
|----|-----------|
|session_id|发送命令用来会话的id|
|element_id|从中获取元素属性的id|
|property_name|CSS特性名称|

### JSON 参数
无

### 响应
css属性的值("字符串")

## 另请参见
* [W3C Specification](https://www.w3.org/TR/webdriver/#dfn-get-element-css-value)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidelementidcsspropertyname)
