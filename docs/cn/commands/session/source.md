# 获得页面源码

获取描述当前应用的层级结构的XML（app）或者页面源码（web）

## 使用样例

```java
// Java
String pageSource = driver.getPageSource();

```

```python
# Python
source = self.driver.page_source

```

```javascript
// Javascript
// webdriver.io example
let source = driver.getPageSource();

// wd example
let pageSource = await driver.source();

```

```ruby
# Ruby
# ruby_lib example
page_source

# ruby_lib_core example
@driver.page_source

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
string pageSource = driver.PageSource;

```

## 描述

在web环境中，source方法返回的是当前窗口的HTML源码。在原生环境(iOS, Android, etc...) 中，source方法返回的是描述应用层级结构的XML。

这个方法对于检查你的应用的层级结构（hierarchy ）并利用结构来写[选择器](/docs/en/commands/element/find-element.md)是有帮助的。

（注意：iOS和Android没有标准方式来定义各自应用源码，所以在调用“获取页面源码”的方法时 ，Appium会遍历应用程序的层次结构（hierarchy）并创建一个XML文档。因此，获取源码操作通常是一项开销很大而且耗时的操作。）

## 支持

### Appium Server

| 平台    | Driver                                                   | 平台版本   | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/remote/RemoteWebDriver.html#getPageSource--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.page_source) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L1808) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/Driver:page_source) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

## HTTP API 规范

### 终端

`GET /session/:session_id/source`

### URL参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|

### JSON参数

None

### 响应

当前环境的源码 (`string`)

## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#dfn-get-page-source)
* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidsource)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019