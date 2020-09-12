# 获得地理位置

获得当前的地理位置

## 使用样例

```java
// Java
Location location = driver.location(); // Must be a driver that implements LocationContext

```

```python
# Python
location = self.driver.location()

```

```javascript
// Javascript
// webdriver.io example
let location = driver.getGeoLocation();

// wd example
let location = await driver.getGeoLocation();

```

```ruby
# Ruby
# ruby_lib example
location

# ruby_lib_core example
@driver.location

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
Location location = driver.Location;

```

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
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/html5/LocationContext.html#location--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L393) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/DriverExtensions/HasLocation#set_location-instance_method) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`GET /session/:session_id/location`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

None


### 响应

| 名称      | 类型     | 描述           |
|----|----|-----------|
| latitude | `number` | 当前的纬度 |
| longitude | `number` | 当前的经度 |
| altitude | `number` | 当前的海拔高度 |


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#sessionsessionidlocation)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019