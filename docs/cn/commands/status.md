[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
# 状态

检索服务器当前状态
[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
## 用法示例

```java
// Java
driver.getStatus();

```

```python
# Python
selenium.webdriver.common.utils.is_url_connectable(port)

```

```javascript
// Javascript
// webdriver.io 示例
driver.status();

// wd 示例
await driver.status();

```

```ruby
# Ruby
# ruby_lib 示例
remote_status

# ruby_lib_core 示例
@driver.remote_status

```

```php
# PHP
// TODO

```

```csharp
// C#
// TODO

```

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
## 介绍

返回有关远端是否处于可创建新会话并且可以另外包含特定实现的元信息的状态信息。

准备就绪状态代表着body的准备情况，当为false的时候，尝试创建一个会话会失败。然而，当值为true的时候并不保证新会话命令将成功

Implementations可以包含其它元信息作为body的一部分，但是顶级属性ready和message是保留的，不能被覆盖。

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
## 支持

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### Appium 服务端

|平台|驱动|平台版本|Appium版本|驱动版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/cn/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/cn/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [Espresso](/docs/cn/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/cn/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/cn/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/cn/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/cn/drivers/windows.md) | 10+ | 1.6.0+ | All |


[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### Appium 客户端

|语言|支持情况|文档地址|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [javadoc.io](https://javadoc.io/page/io.appium/java-client/latest/io/appium/java_client/AppiumDriver.html#getStatus--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.common.utils.is_url_connectable) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L44) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/DriverExtensions/HasRemoteStatus#remote_status-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
## HTTP API 规范

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### 终点

`GET /status`

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### URL 参数

None

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### JSON 参数

None

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
### 返回值

|名称|类型|描述|
|----|----|-----------|
| build.version | `string` | 一个通用的发布标签 (i.e. "2.0rc3") |
| build.revision | `string` | 服务端源代码本地修订版 |

[//]: # (请勿编辑此文件! 这是一个自动生成文件。通过修改/commands-yml/commands/status.yml来编辑此文档)
## 延伸阅读

* [W3C 规范](https://www.w3.org/TR/webdriver/#status)
* [JSONWP 规范](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#status)
