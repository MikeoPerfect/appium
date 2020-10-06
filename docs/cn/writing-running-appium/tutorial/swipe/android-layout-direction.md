## 安卓 'UIScrollable' 滑屏(swipe): 添加滚动布局

滚动页面包括横向滚动和竖向滚动。如果 UIAutomator无法完成自动滚动，显示得声明滚动方向可以解决这个问题。

### 设置滚动布局方向

```java
// setAsVerticalList
// FindElement
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
        "new UiScrollable(new UiSelector().scrollable(true)).setAsVerticalList()" +
         ".scrollIntoView(new UiSelector().text(\"exact_text\"))"));

// setAsHorizontalList
// FindElement
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
        "new UiScrollable(new UiSelector().scrollable(true)).setAsHorizontalList()" +
         ".scrollIntoView(new UiSelector().text(\"exact_text\"))"));

```

