## 滚动(Scroll) / 滑动(Swipe) 教程

### Android 和 iOS 在UI层面的不同

Appium在iOS上使用 XCUITest driver，在Android上使用UIAutomator2, Espresso。Android上默认的driver是UIAutomator2。
iOS环境的默认的驱动设置下，我们可以看到位于可见屏幕之外的元素，但无法与之交互。我们可以检查这些元素的值，但触碰(touch)操作却不可靠。
Android上UIAutomator2的默认设置下，你只能看到当前屏幕的元素。Android 'Espresso' `待补充`。这些表现以及限制来自Apple的XCUITest框架和Android的UIAutomator2框架本身。

当操作元素时，你应该始终记得这些不同之处。

### 简单 滑动(swipe) 操作

1. [滑屏](swipe/simple-screen.md)
2. [元素swipe](swipe/simple-element.md)
3. [半屏 swipe](swipe/simple-partial-screen.md)

### Android: 'UIScrollable' 滑动(swipe)

1. [简单示例](swipe/android-simple.md)
2. [多个滑动视图的例子](swipe/android-multiple.md)
3. [指定滑动布局](swipe/android-layout-direction.md)
4. [技巧和窍门](swipe/android-tricks.md)

### iOS: 'mobile:scroll', 'mobile:swipe' 滑动(swipe)

1. [屏幕swipe](swipe/ios-mobile-screen.md)
2. [元素swipe](swipe/ios-mobile-element.md)
3. [Element search swipe](swipe/ios-mobile-element-search.md)

### iOS: 'pickerWheels' 滑动(swipe)

1. [快速方式 '.setValue()'](swipe/ios-picker-wheels-set-value.md)
2. [慢速方式 'mobile:selectPickerWheelValue'](swipe/ios-picker-wheels-mobile.md)

### Swipe 故障排查手册

1. [滑动(swipe) 故障排查手册](swipe/swipe-troubleshoot-guide.md)

