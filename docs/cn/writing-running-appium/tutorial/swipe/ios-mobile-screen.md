## iOS 'mobile:': 屏幕滑动(swipe)

XCTest框架支持独特的动作操作如"mobile:scroll" 和 "mobile:swipe"。它们不如UIScrollable那么灵活但仍然有用。

更多信息参考[https://developer.apple.com/documentation/xctest/xcuielement]() 文档中'Scrolling' 和 'Performing Gestures' 部分.

通常滑动(swipe)操作完成滑动的动作而滚动(scroll)操作只是尝试更改可见视图而已。

!注意! 滚动方向在滑动(swipe)命令和滚动(scroll)命令中是不同的

```java
/**
 * Performs screen scroll
 *
 * @param dir the direction of scroll
 * @version java-client: 7.3.0
 **/
public void mobileScrollScreenIOS(Direction dir) {
    System.out.println("mobileScrollScreenIOS(): dir: '" + dir + "'"); // always log your actions

    // Animation default time:
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms
    final HashMap<String, String> scrollObject = new HashMap<String, String>();

    switch (dir) {
        case DOWN: // from down to up (! differs from mobile:swipe)
            scrollObject.put("direction", "down");
            break;
        case UP: // from up to down (! differs from mobile:swipe)
            scrollObject.put("direction", "up");
            break;
        case LEFT: // from left to right (! differs from mobile:swipe)
            scrollObject.put("direction", "left");
            break;
        case RIGHT: // from right to left (! differs from mobile:swipe)
            scrollObject.put("direction", "right");
            break;
        default:
            throw new IllegalArgumentException("mobileScrollIOS(): dir: '" + dir + "' NOT supported");
    }
    try {
        driver.executeScript("mobile:scroll", scrollObject); // swipe faster then scroll
        Thread.sleep(ANIMATION_TIME); // always allow swipe action to complete
    } catch (Exception e) {
        System.err.println("mobileScrollIOS(): FAILED\n" + e.getMessage());
        return;
    }
}

/**
 * Performs screen swipe
 *
 * @param dir the direction of swipe
 * @version java-client: 7.3.0
 **/
public void mobileSwipeScreenIOS(Direction dir) {
    System.out.println("mobileSwipeScreenIOS(): dir: '" + dir + "'"); // always log your actions

    // Animation default time:
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms
    final HashMap<String, String> scrollObject = new HashMap<String, String>();

    switch (dir) {
        case DOWN: // from up to down (! differs from mobile:scroll)
            scrollObject.put("direction", "down");
            break;
        case UP: // from down to up  (! differs from mobile:scroll)
            scrollObject.put("direction", "up");
            break;
        case LEFT: // from right to left  (! differs from mobile:scroll)
            scrollObject.put("direction", "left");
            break;
        case RIGHT: // from left to right  (! differs from mobile:scroll)
            scrollObject.put("direction", "right");
            break;
        default:
            throw new IllegalArgumentException("mobileSwipeScreenIOS(): dir: '" + dir + "' NOT supported");
    }
    try {
        driver.executeScript("mobile:swipe", scrollObject);
        Thread.sleep(ANIMATION_TIME); // always allow swipe action to complete
    } catch (Exception e) {
        System.err.println("mobileSwipeScreenIOS(): FAILED\n" + e.getMessage());
        return;
    }
}
```

