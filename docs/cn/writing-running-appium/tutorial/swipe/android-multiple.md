## Android 'UIScrollable' 滑动(swipe): 多个滑动视图的例子

当屏幕有不止一个scrollView时，UIScrollable有可能不能正确地滑动到目标视图。这种情况下我们需要指定目标视图的位置，并设置"new UiSelector().scrollable(true)" 

### 通过 instance 方式

```java
// first scrollView
// FindElement
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
        "new UiScrollable(new UiSelector().scrollable(true).instance(0))" +
         ".scrollIntoView(new UiSelector().text(\"exact_text\"))"));

// second scrollView
// FindElement
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
        "new UiScrollable(new UiSelector().scrollable(true).instance(1))" +
         ".scrollIntoView(new UiSelector().text(\"exact_text\"))"));

```

### 通过 id 方式

```java
// FindElement
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
        "new UiScrollable(new UiSelector().resourceIdMatches(\".*part_id.*\").scrollable(true))" +
         ".scrollIntoView(new UiSelector().text(\"exact_text\"))"));

```


