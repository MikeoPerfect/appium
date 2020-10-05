## iOS 'mobile:': 元素查找滑动

使用下列方式查找元素或滚动视图：
- 使用元素id并指定<code>name</code>参数
- 或使用<code>predicateString</code>参数指定NSPredicate的值

NSPredicate示例参考 [这里](../../ios/ios-predicate.md) 另外，
[https://kapeli.com/cheat_sheets/NSPredicate.docset/Contents/Resources/Documents/index](https://kapeli.com/cheat_sheets/NSPredicate.docset/Contents/Resources/Documents/index)
是一个很好的NSPredicate备忘表。


NSPredicate 定位元素时使用 'name == accessibilityIdentifier'断言参数

```java
String pre = "label == 'exact_text'";
MobileElement el = (MobileElement) driver.findElement(MobileBy.id("element_id"));

mobileScrollToElementIOS(el, pre);

/**
 * Performs element scroll by predicate string
 *
 * @param el  the element to scroll
 * @param pre the predicate string
 * @version java-client: 7.3.0
 **/
public void mobileScrollToElementIOS(MobileElement el, String pre) {
    System.out.println("mobileScrollToElementIOS(): pre: '" + pre + "'"); // always log your actions

    // Animation default time:
    //  - iOS: 200 ms
    // final value depends on your app and could be greater
    final int ANIMATION_TIME = 200; // ms
    final HashMap<String, String> scrollObject = new HashMap<String, String>();
    scrollObject.put("element", el.getId());
    scrollObject.put("predicateString", pre);
    try {
        driver.executeScript("mobile:scroll", scrollObject);
        Thread.sleep(ANIMATION_TIME); // always allow swipe action to complete
    } catch (Exception e) {
        System.err.println("mobileScrollToElementIOS(): FAILED\n" + e.getMessage());
        return;
    }
}
```

'mobileScrollToElementIOS'不能可靠地工作并且在滚动时经常缺少必要的元素，在复杂页面尤其如此。有时将<code>simpleIsVisibleCheck'</code>设置为true也许有帮助。

作为临时方案，可以尝试组合使用简单滚动(屏幕级别或元素级别)并在每一次滚动后检查期望的元素是否在屏幕上可见。

以下为这种组合方式的使用示例：

```java
String pre = "label == 'exact_text'";
mobileScrollScreenByPredicateIOS(pre, Direction.DOWN);

/**
 * Performs screen scroll by predicate string
 *
 * @param pre the predicate string
 * @param dir the direction of swipe
 * @version java-client: 7.3.0
 **/
public void mobileScrollScreenByPredicateIOS(String pre, Direction dir) {
    System.out.println("mobileScrollScreenByPredicateIOS(): dir: '" + dir + "'"); // always log your actions
    final int MAX_SWIPES = 5; // limit maximum swipes

    for (int i = 0; i < MAX_SWIPES; i++) {
        try {
            if (driver.findElement(MobileBy.iOSNsPredicateString(pre)).isDisplayed())
                break;
        } catch (Exception e) {
            // ignore
        }
        mobileScrollScreenIOS(dir);
    }
}
```

