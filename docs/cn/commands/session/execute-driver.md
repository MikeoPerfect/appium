# 执行Driver脚本

针对当前会话（session）运行WebdriverIO脚本，允许在一个Appium请求中执行多条命令。

## 使用样例

```java
// Java
String script = "const el = await driver.$('~foo');\n"
              + "await el.click();"
driver.executeDriverScript(script, new ScriptOptions().withTimeout(200));

```

```python
# Python
# TODO fill out once client code is written

```

```javascript
// Javascript
// webdriver.io example
const script = `
  const el = await driver.$('~foo');
  await el.click();
`;
await driver.executeDriver(script);

// wd example
const script = `
  const el = await driver.$('~foo');
  await el.click();
`;
await driver.executeDriver(script, {timeout: 200});

```

```ruby
# Ruby
# ruby_lib example
# TODO fill out once client code is written

# ruby_lib_core example
# TODO fill out once client code is written

```

```php
# PHP
// TODO PHP sample

```

```csharp
// C#
// TODO C# sample

```

## 描述

Appium的客户机-服务器体系（C/S）结构的一个缺点是每个命令都必须在网络上传输，可能会有很高的延迟。尤其是Appium会话发生在服务提供商的主机上而不是在本地进行的情况下。

这个命令允许将多个命令组成批处理形式，以便在Appium服务器上一次性执行。实现这一点的方法是基于`executeScript`模型：客户端将发送一个表示要执行的代码的字符串。Appium服务器将在当前会话（session）的上下文中执行该代码，并返回脚本指定的任何值。

这个命令接收三个参数（每个客户端可能以其自己的方式收集）：

  * `script`：由脚本本身组成的字符串
  * `timeout`：表示在终止运行程序脚本的进程之前要等待的毫秒数。默认值等于1小时。
  * `type`：表示脚本所使用的语言或API的类型的字符串。现在只支持一种类型，`webdriveio`。

Not just any code can run in this context. The code must be written in Javascript, and it will have access to a context with three objects

并不是任意代码都能在这个环境中运行。代码必须用JavaScript编写，并可以访问有以下三个对象的环境。

  * `driver`：[WebdriverIO](https://webdriver.io/) driver对象。可以假设这个driver已经与Appium server建立连接并已经可以执行命令。安装使用的WebdriverIO版本是根据 `appium-base-driver`的 `package.json`中指定的版本。
  * `console`： 一个有`log`, `warn`和 `error`方法的定制`console`对象，可以进行日志记录。
  * `Promise`: 一个Promise库 ([Bluebird](http://bluebirdjs.com/docs/getting-started.html)), 用来简化异步操作。

代码会下面的例子所示，放在一个`async`函数中，所以你可以随意使用`await`：

```js
(async function (driver, console, Promise) {
  // --> your script here <--
})()
```

任何错误都会导致给命令的调用方一个错误类型的响应。任何返回值都会被按照下面的形式进行包装并返回给客户端：

```js
{result: <return value>, logs: {log: [], warn: [], error: []}}
```

使用响应对象，你可以同时获得返回值以及你编写的所有日志语句。

The advantage of this approach of using WebdriverIO code is that you have access to a full programming language and Appium API, and can use any language or API features you need, including loops, conditionals, and explicit waits. The WebdriverIO API cannot be enumerated here, so visit the [WebdriverIO documentation](https://webdriver.io/docs/api.html) for more info.

这样使用WebdriverIO代码的方法的优势在于，你可以使用完整的编程语言和Appium API，并且可以使用任何你需要的语言或API特性，包括循环、条件语句和显式等待。无法在这里列举webdririo API，因此请访问[WebdriverIO 文档](https://webdriver.io/docs/api.html)以获取更多信息。

## 支持

### Appium Server

| 平台    | Driver                                                   | 平台版本   | Appium版本 | Driver版本 |
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | 8.0 to 9.3 | All | All |
| Android | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | 4.3+ | All | All |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |

### Appium客户端

| 语言                                                         | 支持版本 | 文档                                                         |
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [javadoc.io](https://javadoc.io/page/io.appium/java-client/latest/io/appium/java_client/ExecutesDriverScript.html#executeDriverScript-java.lang.String-io.appium.java_client.driverscripts.ScriptOptions-) |
|[Python](https://github.com/appium/python-client/releases/latest)| None |  |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| None |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| None |  |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| None |  |
|[PHP](https://github.com/appium/php-client/releases/latest)| None |  |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| None |  |

## HTTP API规范

### 终端

`POST /session/:session_id/appium/execute_driver`

### URL参数

| 名称       | 描述                            |
|----|-----------|
|session_id|将指令发往的会话（session）的ID|

### JSON参数

| 名称    | 类型     | 描述                                                         |
|----|----|-----------|
| script | `string` | 需要执行的webdriverio脚本 |
| type | `string` | 脚本类型名称。现在只支持 'webdriverio' |
| timeout | `number` | Appium应该等待脚本执行完成的毫秒值。超过这个时间，Appium会由于超时而终止脚本的执行。 |

### 响应

脚本的执行结果。结果包含两部分：`result` and `logs`。result是脚本执行后的返回值。logs包含脚本输出在控制台中的所有内容。 (`any`)

## 参考

无



本文由 [KangarooChen](https://github.com/KangarooChen) 翻译，Last english version: 1be5bd8c1e22fe46188dd9c498766ae587c88887, 4 Mar 2020