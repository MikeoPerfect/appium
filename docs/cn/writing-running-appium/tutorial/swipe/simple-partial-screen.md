## 简单的半屏swipe

有些场景我们只需要屏幕的小区域进行swipe动作：
1. 使用iOS的'mobile:scroll'进行精确地滚动失败。
2. 考虑到速度因素：触摸滚动比任何swipe方法都要快。

(这种情况下)我们可以使用现有的swipe操作，从屏幕中心开始并减少执行的次数。

```java
/**
 * Performs small swipe from the center of screen
 *
 * @param dir the direction of swipe
 * @version java-client: 7.3.0
 **/
public void swipeScreenSmall(Direction dir) {
    System.out.println("swipeScreenSmall(): dir: '" + dir + "'"); // always log your actions

    // Animation default time:
    //  - Android: 300 ms
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms

    final int PRESS_TIME = 200; // ms

    PointOption pointOptionStart, pointOptionEnd;

    // init screen variables
    Dimension dims = driver.manage().window().getSize();

    // init start point = center of screen
    pointOptionStart = PointOption.point(dims.width / 2, dims.height / 2);

    // reduce swipe move into multiplier times comparing to swipeScreen move
    int mult = 10; // multiplier
    switch (dir) {
        case DOWN: // center of footer
            pointOptionEnd = PointOption.point(dims.width / 2, (dims.height / 2) + (dims.height / 2) / mult);
            break;
        case UP: // center of header
            pointOptionEnd = PointOption.point(dims.width / 2, (dims.height / 2) - (dims.height / 2) / mult);
            break;
        case LEFT: // center of left side
            pointOptionEnd = PointOption.point((dims.width / 2) - (dims.width / 2) / mult, dims.height / 2);
            break;
        case RIGHT: // center of right side
            pointOptionEnd = PointOption.point((dims.width / 2) + (dims.width / 2) / mult, dims.height / 2);
            break;
        default:
            throw new IllegalArgumentException("swipeScreenSmall(): dir: '" + dir.toString() + "' NOT supported");
    }
        
    // execute swipe using TouchAction
    try {
        new TouchAction(driver)
                .press(pointOptionStart)
                // a bit more reliable when we add small wait
                .waitAction(WaitOptions.waitOptions(Duration.ofMillis(PRESS_TIME)))
                .moveTo(pointOptionEnd)
                .release().perform();
    } catch (Exception e) {
        System.err.println("swipeScreenSmall(): TouchAction FAILED\n" + e.getMessage());
        return;
    }

    // always allow swipe action to complete
    try {
        Thread.sleep(ANIMATION_TIME);
    } catch (InterruptedException e) {
        // ignore
    }
}
```

