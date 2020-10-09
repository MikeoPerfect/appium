## 简单的屏幕swipe

Swipe操作有起始和终止点。起始点位置很重要。以下元素可能会阻止swipe动作生效：

- 应用接口/菜单，例如 页眉（header）或页脚（footer）。
- 等待被触碰(tap)的元素并没有将touch事件传递给滚动视图

最好从屏幕中间开始swipe动作以获取更稳定的效果。

![swipe_screen](images/simple-screen.png)

```java
/**
 * Performs swipe from the center of screen
 *
 * @param dir the direction of swipe
 * @version java-client: 7.3.0
 **/
public void swipeScreen(Direction dir) {
    System.out.println("swipeScreen(): dir: '" + dir + "'"); // always log your actions

    // Animation default time:
    //  - Android: 300 ms
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms

    final int PRESS_TIME = 200; // ms

    int edgeBorder = 10; // better avoid edges
    PointOption pointOptionStart, pointOptionEnd;

    // init screen variables
    Dimension dims = driver.manage().window().getSize();

    // init start point = center of screen
    pointOptionStart = PointOption.point(dims.width / 2, dims.height / 2);

    switch (dir) {
        case DOWN: // center of footer
            pointOptionEnd = PointOption.point(dims.width / 2, dims.height - edgeBorder);
            break;
        case UP: // center of header
            pointOptionEnd = PointOption.point(dims.width / 2, edgeBorder);
            break;
        case LEFT: // center of left side
            pointOptionEnd = PointOption.point(edgeBorder, dims.height / 2);
            break;
        case RIGHT: // center of right side
            pointOptionEnd = PointOption.point(dims.width - edgeBorder, dims.height / 2);
            break;
        default:
            throw new IllegalArgumentException("swipeScreen(): dir: '" + dir + "' NOT supported");
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
        System.err.println("swipeScreen(): TouchAction FAILED\n" + e.getMessage());
        return;
    }

    // always allow swipe action to complete
    try {
        Thread.sleep(ANIMATION_TIME);
    } catch (InterruptedException e) {
        // ignore
    }
}

public enum Direction {
    UP,
    DOWN,
    LEFT,
    RIGHT;
}
```


