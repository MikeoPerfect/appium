## Swipe 故障排查手册

### 简单 swipe 动作

采用以下步骤进行故障排查：

1. 添加触摸点坐标的日志

带有日志的滑屏操作示例:

```java
/**
 * Performs swipe from the center of screen
 *
 * @param dir the direction of swipe
 * @version java-client: 7.3.0
 **/
public void swipeScreenWithLogs(Direction dir) {
    System.out.println("swipeScreen(): dir: '" + dir + "'"); // 总在日志中记录执行的操作

    // 默认动画时长:
    //  - Android: 300 ms
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms

    final int PRESS_TIME = 200; // ms

    int edgeBorder = 10; // better avoid edges
    Point pointStart, pointEnd;
    PointOption pointOptionStart, pointOptionEnd;

    // init screen variables
    Dimension dims = driver.manage().window().getSize();

    // init start point = center of screen
    pointStart = new Point(dims.width / 2, dims.height / 2);

    switch (dir) {
        case DOWN: // center of footer
            pointEnd = new Point(dims.width / 2, dims.height - edgeBorder);
            break;
        case UP: // center of header
            pointEnd = new Point(dims.width / 2, edgeBorder);
            break;
        case LEFT: // center of left side
            pointEnd = new Point(edgeBorder, dims.height / 2);
            break;
        case RIGHT: // center of right side
            pointEnd = new Point(dims.width - edgeBorder, dims.height / 2);
            break;
        default:
            throw new IllegalArgumentException("swipeScreen(): dir: '" + dir.toString() + "' NOT supported");
    }

    // execute swipe using TouchAction
    pointOptionStart = PointOption.point(pointStart.x, pointStart.y);
    pointOptionEnd = PointOption.point(pointEnd.x, pointEnd.y);
    System.out.println("swipeScreen(): pointStart: {" + pointStart.x + "," + pointStart.y + "}");
    System.out.println("swipeScreen(): pointEnd: {" + pointEnd.x + "," + pointEnd.y + "}");
    System.out.println("swipeScreen(): screenSize: {" + dims.width + "," + dims.height + "}");
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
```

示例输出:

```
swipeScreen(): dir: 'DOWN'
swipeScreen(): pointStart: {187,333}
swipeScreen(): pointEnd: {187,657}
swipeScreen(): screenSize: {375,667}
swipeScreen(): dir: 'UP'
swipeScreen(): pointStart: {187,333}
swipeScreen(): pointEnd: {187,10}
swipeScreen(): screenSize: {375,667}
```

2. Android设置里开启'显示Taps位置'和'指针位置'，在'设置 -> 系统 -> 开发者选项 -> tab输入'显示操作的位置坐标.
3. 手动执行相同的滑屏动作以验证。

### Android: 'UIScrollable' 滑动(swipe)

#### 滑动没有开始：

1. 检查是否有多个滑动视图(scrollViews). 如果有多个，通过instance/resource-id/classname/等方式指定具体的某一个。   
2. 检查滑动视图的布局方向，使用'setAsVerticalList'或'setAsHorizontalList'来设置布局方向。
3. 混合使用上述两种方式。
4. 都失败的话，尝试使用简单元素滑动方式。

#### 找不到查找的元素:

1. 查找前添加暂停动作，在此期间手动滑屏让查找的元素出现。暂停后添加代码检查是否可以找到元素。下面的例子使用文本查找方式来演示——
   

```java
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
         "new UiSelector().text(\"exact_text\")"));
// or
MobileElement element = (MobileElement) driver.findElement(MobileBy.AndroidUIAutomator(
         "new UiSelector().textContains(\"part_text\")"));

try {
    System.out.println("Element found: " + !element.getId().isEmpty());
} catch (Exception e) {
    System.out.println("Element found: false");
}
```

### iOS: 'mobile:scroll', 'mobile:swipe' 滑动(swipe)

#### 滑动没有开始：

1. 检查方向，注意'scroll'和'swipe'方法的方向参数不同。
2. 都失败的话，尝试使用简单元素滑动方式。

#### 找不到查找的元素:

1. 尝试使用精准swipe而不是scroll方法
2. 有时当查找的元素只出现一部分的话，tap动作将可能失败。此时，使用简单部分元素滑动(Simple-partial-element)——就像在简单半屏例子种演示的那样——中的策略重试一下。同时执行部分元素滑动(partial element swipe)操作后，再重试一下tap动作。
