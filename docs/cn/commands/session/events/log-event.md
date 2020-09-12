# 记录事件

存储一个自定义事件

## 使用示例

```java
// Java
CustomEvent evt = new CustomEvent();
evt.setEventName("funEvent");
evt.setVendor("appium");
driver.logEvent(evt);

```

```python
# Python
driver.log_event('appium', 'funEvent')

```

```javascript
// Javascript
// webdriver.io example
driver.logEvent('appium', 'funEvent')

// wd example
// WD code here

```

```ruby
# Ruby
# ruby_lib example
driver.log_event vendor: 'appium', event: 'funEvent'

# ruby_lib_core example
@driver.logs.event vendor: 'appium', event: 'funEvent'
@driver.logs.event = { vendor: 'appium', event: 'anotherEvent' }

```

```php
# PHP
// PHP Code here

```

```csharp
// C#
// csharp Code here

```


## 描述

此API允许我们存储一个自定义的事件。

Appium提供[Appium Event Timing](/advanced-concepts/event-timings/)来追踪事件何时发生。

自定义事件特性允许用户将一个自定义事件作为特性来存储。

## 支持


### Appium Server

| 平台    | Driver                                                   | 平台版本   | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.16.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | 1.16.0+ | All |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.16.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.16.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | 1.16.0+ | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.16.0+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.16.0+ | All |

### Appium客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebElement.html#click--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.log_event.LogEvent.log_event) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| None |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| None | [github.com](https://github.com/admc/wd/releases) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/appium_lib/Appium/Driver#log_event-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/releases/latest) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium) |


## HTTP API 规范


### 终端

`POST /session/:session_id/appium/log_event`


### URL参数

None


### JSON参数

| 名称   | 类型     | 描述                                                      |
|----|----|-----------|
| vendor | `string` | 事件提供者的名字。会出现在 `vendor:event`中`vendor`的位置 |
| event | `string` | 事件的名字。 会出现在 `vendor:event`中`event`的位置 |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L600)
* [add new route to allow logging of custom events](https://github.com/appium/appium-base-driver/pull/364)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 2b60bef0264515c912137d038c8f64e580050497, 11 May 2020