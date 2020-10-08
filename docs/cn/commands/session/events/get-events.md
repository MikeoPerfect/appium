# 获取事件

获取存储在Appium服务端的事件

## 使用样例

```java
// Java
driver.getEvents();

```

```python
# Python
driver.get_events()
driver.get_events(['event1', 'event2'])

```

```javascript
// Javascript
// webdriver.io example
browser.getEvents(['event'])

// wd example
// WD code here

```

```ruby
# Ruby
# ruby_lib example
driver.log_events
driver.log_events('event')
driver.log_events(['event1', 'event2'])

# ruby_lib_core example
@driver.logs.events
@driver.logs.events('event')
@driver.logs.events(['event1', 'event2'])

```

```php
# PHP
// PHP Code here

```

```csharp
// C#
// csharp code here

```

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
|[Python](https://github.com/appium/python-client/releases/latest)| All | [appium.github.io](https://appium.github.io/python-client-sphinx/webdriver.extensions.html#webdriver.extensions.log_event.LogEvent.get_events) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| None |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| None | [github.com](https://github.com/admc/wd/releases) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/appium_lib/Appium/Driver#log_event-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| None | [github.com](https://github.com/appium/php-client/releases/latest) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None | [github.com](https://github.com/appium/appium) |


## HTTP API 规范

终端

`POST /session/:session_id/appium/events`


### URL参数

None


### JSON参数

| 名称 | 类型                   | 描述                                             |
|----|----|-----------|
| type | `string|array<string>` | （可选）如果提供了type参数，获取type中指定的事件 |


### 响应

事件的JSON对象，比如：`{'commands' => [{'cmd' => 123455, ....}], 'startTime' => 1572954894127, }`。如果提供type参数，JSON中的对象是经过type过滤的。


## 参考

* [JSONWP Specification](https://github.com/appium/appium-base-driver/blob/master/lib/protocol/routes.js#L597)
* [add ability to retrieve log events as a new api route](https://github.com/appium/appium-base-driver/pull/365)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 2b60bef0264515c912137d038c8f64e580050497, 11 May 2020