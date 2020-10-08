
# Actions

执行一个或多个键盘和触控（触摸、鼠标、手写笔）操作

## 使用样例

```java
// Java
WebElement source = (MobileElement) driver.findElementsByAccessibilityId("SomeAccessibilityID");
WebElement target = (MobileElement) driver.findElementsByAccessibilityId("SomeOtherAccessibilityID");

Point source = dragMe.getCenter();
Point target = driver.findElementByAccessibilityId("dropzone").getCenter();
PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
Sequence dragNDrop = new Sequence(finger, 1);
dragNDrop.addAction(finger.createPointerMove(Duration.ofMillis(0),
                    PointerInput.Origin.viewport(), source.x, source.y));
dragNDrop.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
dragNDrop.addAction(finger.createPointerMove(Duration.ofMillis(700),
                    PointerInput.Origin.viewport(),target.x, target.y));
dragNDrop.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
driver.perform(Arrays.asList(dragNDrop));

```

```python
# Python
element = driver.find_element_by_accessibility_id("elId")
actions = ActionChains(driver)
actions.move_to_element(element)
actions.click(hidden_submenu)
actions.perform()

```

```javascript
// Javascript
// webdriver.io example
// Example: expressing a 1-second pinch-and-zoom
// with a 500ms wait after the fingers first touch:
driver.performActions([{
    "type": "pointer",
    "id": "finger1",
    "parameters": {"pointerType": "touch"},
    "actions": [
        {"type": "pointerMove", "duration": 0, "x": 100, "y": 100},
        {"type": "pointerDown", "button": 0},
        {"type": "pause", "duration": 500},
        {"type": "pointerMove", "duration": 1000, "origin": "pointer", "x": -50, "y": 0},
        {"type": "pointerUp", "button": 0}
    ]
}, {
    "type": "pointer",
    "id": "finger2",
    "parameters": {"pointerType": "touch"},
    "actions": [
        {"type": "pointerMove", "duration": 0, "x": 100, "y": 100},
        {"type": "pointerDown", "button": 0},
        {"type": "pause", "duration": 500},
        {"type": "pointerMove", "duration": 1000, "origin": "pointer", "x": 50, "y": 0},
        {"type": "pointerUp", "button": 0}
    ]
}]);

// release an action
driver.releaseActions();

// wd example
// Performs a 'pinch-and-zoom'
var actions = new wd.W3CActions(driver);
var touchInput = actions.addTouchInput();
touchInput.pointerMove({duration: 0, x: 100, y: 100});
touchInput.pointerDown({button: 0});
touchInput.pause({duration: 500});
touchInput.pointerMove({duration: 1000, origin: 'pointer', x: -50, y: 100});
touchInput.pointerUp({button: 0});
var secondTouchInput = actions.addTouchInput();
secondTouchInput.pointerMove({duration: 0, x: 200, y: 200});
secondTouchInput.pointerDown({button: 0});
secondTouchInput.pause({duration: 300});
secondTouchInput.pointerMove({duration: 1000, origin: 'pointer', x: 50, y: 100});
secondTouchInput.pointerUp({button: 0});
await actions.perform();

// Releases any previously run actions (e.g.: if a key is 'down' because of /actions, releases it using key up)
await driver.releaseW3CActions();

```

```ruby
# Ruby
# ruby_lib example
# Send keys to an element
# Build Single action chain
action_builder = action
keyboard = action_builder.key_inputs
el = find_element(id: "some_id")
action.click(el).pause(keyboard).pause(keyboard).pause(keyboard).send_keys('keys').perform

# Build multiple action chains
# Example: expressing a 1-second pinch-and-zoom
# with a 500ms wait after the fingers first touch:
f1 = action.add_pointer_input(:touch, 'finger1')
f1.create_pointer_move(duration: 1, x: 200, y: 500, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f1.create_pointer_down(:left)
f1.create_pause(0.5)
f1.create_pointer_move(duration: 1, x: 200, y: 200, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f1.create_pointer_up(:left)

f2 = action.add_pointer_input(:touch, 'finger2')
f2.create_pointer_move(duration: 1, x: 200, y: 500, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f2.create_pointer_down(:left)
f2.create_pause(0.5)
f2.create_pointer_move(duration: 1, x: 200, y: 800, origin: ::Selenium::Web@Driver::Interactions::PointerMove::VIEWPORT)
f2.create_pointer_up(:left)

perform_actions [f1, f2]

# ruby_lib_core example
# Send keys to an element
# Build Single action chain
action_builder = @driver.action
keyboard = action_builder.key_inputs
el = @driver.find_element(id: "some_id")
@driver.action.click(el).pause(keyboard).pause(keyboard).pause(keyboard).send_keys('keys').perform

# Build multiple action chains
# Example: expressing a 1-second pinch-and-zoom
# with a 500ms wait after the fingers first touch:
f1 = @driver.action.add_pointer_input(:touch, 'finger1')
f1.create_pointer_move(duration: 1, x: 200, y: 500, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f1.create_pointer_down(:left)
f1.create_pause(0.5)
f1.create_pointer_move(duration: 1, x: 200, y: 200, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f1.create_pointer_up(:left)

f2 = @driver.action.add_pointer_input(:touch, 'finger2')
f2.create_pointer_move(duration: 1, x: 200, y: 500, origin: ::Selenium::WebDriver::Interactions::PointerMove::VIEWPORT)
f2.create_pointer_down(:left)
f2.create_pause(0.5)
f2.create_pointer_move(duration: 1, x: 200, y: 800, origin: ::Selenium::Web@Driver::Interactions::PointerMove::VIEWPORT)
f2.create_pointer_up(:left)

@driver.perform_actions [f1, f2]

```

```php
# PHP
// TODO

```

```csharp
// C#
var inputDevice = new PointerInputDevice(PointerKind.Touch);
var actionSequence = new ActionSequence(inputDevice, 0);

actionSequence.AddAction(inputDevice.CreatePointerMove(element));
actionSequence.AddAction(inputDevice.CreatePointerDown(PointerButton.TouchContact));
actionSequence.AddAction(inputDevice.CreatePause(TimeSpan.FromSeconds(1)));
actionSequence.AddAction(inputDevice.CreatePointerUp(PointerButton.TouchContact));

driver.PerformActions(new List<ActionSequence> {actionSequence});

```


## 描述

* input source: 表示一系列操作被分派到的输入设备（指针或键）。输入源具有唯一的ID。
* action: 分派到输入源的操作。 对于键盘源，操作行为可以是“ keyDown”或“ keyUp”。 对于指针事件，可以是“pointerMove”，“pointerDown”或“pointerUp”。 “pause”事件也可以发送到设备。

The Actions API会获取输入源列表，并执行每个”tick”。一个 “tick”是动作链的一部分，因此，如果您有两个输入源，那么第一个”tick”是索引为0的动作，第二个“tick”是索引为1的动作，依此类推。所有动作的每个“tick“均同时执行。



## 支持


### Appium Server

|平台|Driver|平台版本|Appium版本|Driver版本|
|--------|----------------|------|--------------|--------------|
| iOS | [XCUITest](/docs/en/drivers/ios-xcuitest.md) | 9.3+ | 1.6.0+ | All |
|  | [UIAutomation](/docs/en/drivers/ios-uiautomation.md) | None | None | None |
| Android | [Espresso](/docs/en/drivers/android-espresso.md) | ?+ | 1.9.0+ | All |
|  | [UiAutomator2](/docs/en/drivers/android-uiautomator2.md) | ?+ | 1.6.0+ | All |
|  | [UiAutomator](/docs/en/drivers/android-uiautomator.md) | None | None | None |
| Mac | [Mac](/docs/en/drivers/mac.md) | ?+ | 1.6.4+ | All |
| Windows | [Windows](/docs/en/drivers/windows.md) | 10+ | 1.6.0+ | All |



### Appium 客户端

|语言|支持|文档|
|--------|-------|-------------|
|[Java](https://github.com/appium/java-client/releases/latest)| All | [seleniumhq.github.io](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/interactions/Actions.html) |
|[Python](https://github.com/appium/python-client/releases/latest)| All | [selenium-python.readthedocs.io](https://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.common.action_chains) |
|[Javascript (WebdriverIO)](http://webdriver.io/index.html)| All |  |
|[Javascript (WD)](https://github.com/admc/wd/releases/latest)| All |  |
|[Ruby](https://github.com/appium/ruby_lib/releases/latest)| All | [www.rubydoc.info](https://www.rubydoc.info/gems/selenium-webdriver/Selenium/WebDriver/W3CActionBuilder) |
|[PHP](https://github.com/appium/php-client/releases/latest)| All | [github.com](https://github.com/jupeter/selenium-php-webdriver/blob/master/Webdriver/Common/ActionChains.php) |
|[C#](https://github.com/appium/appium-dotnet-driver/releases/latest)| All | [github.com](https://github.com/appium/appium-dotnet-driver/) |


## HTTP API 规范


### 终端

`POST /session/:sessionId/actions`


### URL 参数

|名称|描述|
|----|-----------|
|session_id|将指令发往的会话（session）的ID|


### JSON 参数

|名称|类型|描述|
|----|----|-----------|
| actions | `array<array>` | 一系列输入源 |
| actions[$INDEX] | `object` | 代表输入源的对象 |
| actions[$INDEX].type | `string` | 输入源的类型。 可以是“point”，“key”或“null” |
| actions[$INDEX].id | `string` | 输入设备的唯一标识符，用于当前和将来的操作 |
| actions[$INDEX].parameters | `object` | 可选）设置输入源的参数。 “pointer”是必须输入项 |
| actions[$INDEX].parameters.pointerType | `string` | 指针类型。 可以是“touch”，“mouse”或“pen” |
| actions[$INDEX].actions | `array<object>` | 在输入源上执行的操作的列表 |
| actions[$INDEX].actions | `array<object>` | 在输入源上执行的操作的列表 |
| actions[$INDEX].actions[$INDEX] | `object` | 在输入源上执行的操作 |
| actions[$INDEX].actions[$INDEX].type | `string` | 操作类型。 对于任何输入源，都可以“pause”。 对于“pointer”，输入源为“ pointerMove”，“ pointerUp”或“ pointerDown”。 对于“key”，它可以是“ keyDown”或“ keyUp” |
| actions[$INDEX].actions[$INDEX].value | `string` | 对于“ keyUp”或“ keyDown”操作，该值将发送到键盘。 应该是一个字符的字符串（“ s”，“ \ uE009”） |
| actions[$INDEX].actions[$INDEX].duration | `number` | 以“ ms”为单位执行操作的时间。 仅适用于“pause”和“pointerMov”。 |
| actions[$INDEX].actions[$INDEX].origin | `string|object` | 对于'pointerMove'，它告诉输入源x，y是相对的。 可以是“viewport”，“pointe”或\{'element-6066-11e4-a52e-4f735466cecf'&#58; '<ELEMENT_ID>'\} |
| actions[$INDEX].actions[$INDEX].x | `number` | 指针移动事件的X坐标 |
| actions[$INDEX].actions[$INDEX].y | `number` | 指针移动事件的Y坐标 |


### 响应

null


## 参考

* [W3C Specification](https://www.w3.org/TR/webdriver/#actions)
