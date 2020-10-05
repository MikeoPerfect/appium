## Android 'UIScrollable' 滑动: 技巧和窍门

尽管Appium不允许你直接使用'UIScrollable'的所有能力，但可以通过忽略错误的技巧来充分利用'UIScrollable'的能力。

### 向前滚动

```java
// scrollForward (精确滑动一个视图)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).scrollForward()"));
} catch (InvalidSelectorException e) {
    // ignore
}

// flingForward (快速滑动)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).flingForward()"));
} catch (InvalidSelectorException e) {
    // ignore
}
```

### 向后滚动

```java
// scrollBackward (精确滑动一个视图)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).scrollBackward()"));
} catch (InvalidSelectorException e) {
    // ignore
}

// flingBackward (快速滑动)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).flingBackward()"));
} catch (InvalidSelectorException e) {
    // ignore
}
```

### 滑到开始位置

```java
// scrollToBeginning (每次滑动一个视图，最多滑10次)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).scrollToBeginning(10)"));
} catch (InvalidSelectorException e) {
    // ignore
}

// flingToBeginning (快速滑动，最多滑10次)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).flingToBeginning(10)"));
} catch (InvalidSelectorException e) {
    // ignore
}
```

### 滑到结束位置

```java
// scrollToEnd (每次滑动一个视图，最多滑10次)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).scrollToEnd(10)"));
} catch (InvalidSelectorException e) {
    // ignore
}

// flingToEnd (快速滑动，最多滑10次)
try {
    driver.findElement(MobileBy.AndroidUIAutomator(
            "new UiScrollable(new UiSelector().scrollable(true)).flingToEnd(10)"));
} catch (InvalidSelectorException e) {
    // ignore
}
```

