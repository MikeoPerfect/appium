# 设置剪贴板

设置系统剪贴板内容
## 使用样例

```java
// Java
// base64Content is Base64-encoded content
driver.setClipboard("label", ClipboardContentType.PLAINTEXT, base64Content);
driver.setClipboardText("happy testing");

```

```python
# Python
self.driver.set_clipboard('happy testing')
self.driver.set_clipboard_text('happy testing')

```

```javascript
// Javascript
// webdriver.io example
driver.setClipboard('happy testing', 'plaintext')

// wd example
await driver.setClipboard('happy testing', 'plaintext')

```

```ruby
# Ruby
# ruby_lib example
set_clipboard content: 'happy testing'

# ruby_lib_core example
@driver.set_clipboard content: 'happy testing'

```

```php
# PHP
// PHP Code here

```

```csharp
// C#
// CSharp Code here

```


## 支持

### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | None | None | None |
| Mac | [Mac](/docs/en/drivers/mac.md) | None | None | None |
| Windows | [Windows](/docs/en/drivers/windows.md) | None | None | None |


### Appium Clients

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html#click--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.clipboard.Clipboard.get_clipboard) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/releases) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [iOS](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Ios/Device#set_clipboard-instance_method) [Android](https://www.rubydoc.info/github/appium/ruby_lib_core/Appium/Core/Android/Device#set_clipboard-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/releases/latest) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium) |

## HTTP API 规范

### 终端

`POST /session/:session_id/appium/device/set_clipboard`

### URL 参数

|名称|描述|
|----|-----------|
|session_id|将命令路由到服务器的sessionID|

### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| content | `String` | 实际base64编码的剪贴板内容 |
| contentType | `string` | 要获取的内容的类型。纯文本，图像，URL。 Android仅支持纯文本 |
| label | `string` | 用于Android的剪贴板数据标签 |

### 响应

来自 Appium server 的响应(`string`)

## 参考

None