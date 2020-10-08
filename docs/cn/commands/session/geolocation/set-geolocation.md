# 设置地理位置

设置当前的地理位置

## 使用样例

```java
// Java
driver.setLocation(new Location(49, 123, 10)); // Must be a driver that implements LocationContext

```

```python
# Python
self.driver.set_location(49, 123, 10)

```

```javascript
// Javascript
// webdriver.io example
driver.setGeoLocation({latitude: "121.21", longitude: "11.56", altitude: "94.23"});

// wd example
await driver.setGeoLocation(121.21, 11.56, 10);

```

```ruby
# Ruby
# ruby_lib example
set_location(121.21, 11.56, 94.23)

# ruby_lib_core example
@driver.set_location(121.21, 11.56, 94.23)

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
driver.Location.Altitude = 94.23;
driver.Location.Latitude = 121.21;
driver.Location.Longitude = 11.56;

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

### Appium 客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/html5/LocationContext.html#location--) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](http://selenium-python.readthedocs.io/api.html) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All | [github.com](https://github.com/admc/wd/blob/master/lib/commands.js#L407) |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium%2FWebDriver%2FDriverExtensions%2FHasLocation:set_location) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/appium/php-client/) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:session_id/location`


### URL 参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON Parameters

| 名称      | 类型     | 描述                                                        |
|----|----|-----------|
| latitude | `number` | 想要设置的纬度 |
| longitude | `number` | 想要设置的经度 |
| altitude | `number` | 想要设置的海报高度 (可选。 海拔高度仅在Android真机上生效。) |


### 响应

null


## 参考

* [JSONWP Specification](https://github.com/SeleniumHQ/selenium/wiki/JsonWireProtocol#post-sessionsessionidlocation)



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: d05573600bb3ef2663a9c1e37a02c2ff5ec62155, 31 Dec 2019