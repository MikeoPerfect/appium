## iOS 输入事件的底层视角


### 什么是输入事件？

iOS 使用事件这个概念来处理从不同输入设备收到的信号。一个事件就是一个对象，由某个输入设备的某个信号对应产生。
然后，这些对象被投递到对应的内核子系统，经过处理之后，通知所有监听的进程，比如，tap，点击，滑动等。
这就意味着为了模拟外部设备生成的信号，比如触摸屏幕，只需要按真实设备生成事件的顺序，发送有相同属性的事件对象，


### 让我们模拟一个单点击事件

该事件的API是苹果的私有API之一，不开源也没有任何文档。XCTest 尽管如此，还是有可能通过XCTest没有文档的私有接口来生成事件。我们对[XCPointerEventPath](https://github.com/appium/WebDriverAgent/blob/master/PrivateHeaders/XCTest/XCPointerEventPath.h) 和 [XCSynthesizedEventRecord](https://github.com/appium/WebDriverAgent/blob/master/PrivateHeaders/XCTest/XCSynthesizedEventRecord.h) 接口特别感兴趣。
这些接口允许我们创建输入事件链，并提供给系统内核执行。

为了合成单机事件，我们必须：
- 创建一个 `XCPointerEventPath` 实例，然后初始化为`在初始点触摸`。
- 使用 `liftUpAtOffset:` 方法，给每个实例添加一个 `liftUp` 事件，偏移量为：`0.125s`。
- 使用`addPointerEventPath:`方法，添加生成的事件对象给`XCSynthesizedEventRecord` 实例。
- 使用`XCSynthesizedEventRecord`的`synthesizeWithError:`方法来执行事件，并处理返回的错误信息。

对于这些 API，有如下限制：
- 每个 `XCPointerEventPath` 实例只能执行一个动作。举个例子，如果想给一个实例添加两个点击事件，都会被忽略掉。
- 每个 `XCPointerEventPath` 实例都只能用特定的点击类型来初始化，比如，touch, mouse (从 Xcode 10.2开始) 或者 keyboard (从 Xcode 10.2)
- 对一个已经存在的 `XCPointerEventPath` 实例，事件只能增加偏移量。


### 更加复杂的动作事件怎么办？

不幸的是，这些接口是私有的，没有任何文档。
我们只能通过尝试组合不同的输入，才能搞清楚究竟有了什么效果。目前所知的是，在多个`XCPointerEventPath`实例之间叠加时间，会生成多点触控事件，有多少事件实例，就有多少手指。
所以，为了生成二指滑动事件，我们需要提供如下事件：

- 创建两个 `XCPointerEventPath` 实例， 然后初始化为`在初始点触摸`。
- 使用`moveToPoint:`方法，给每个实例添加`moveToPoint`事件，偏移量为：`0.525s`。
- 使用 `liftUpAtOffset:` 方法，给每个实例添加一个 `liftUp` 事件，偏移量为：`0.525s`。
- 使用`addPointerEventPath:`方法，添加生成的事件对象给`XCSynthesizedEventRecord` 实例。
- 使用`XCSynthesizedEventRecord`的`synthesizeWithError:`方法来执行事件，并处理返回的错误信息。

### 拓展阅读

不幸的是，该主题根本就没有太多的信息（私有 API `¯\_(ツ)_/¯`）. 可以参考如下的资料：

- https://github.com/appium/WebDriverAgent/tree/master/PrivateHeaders/XCTest
- https://github.com/appium/WebDriverAgent/blob/master/WebDriverAgentTests/IntegrationTests/FBW3CTouchActionsIntegrationTests.m
- https://github.com/appium/WebDriverAgent/blob/master/WebDriverAgentTests/IntegrationTests/FBW3CMultiTouchActionsIntegrationTests.m
- https://github.com/appium/WebDriverAgent/blob/master/WebDriverAgentLib/Utilities/FBW3CActionsSynthesizer.m
