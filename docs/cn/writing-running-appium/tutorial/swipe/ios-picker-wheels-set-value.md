## iOS pickerWheels: 快速方式 '.setValue()' 示例

不幸的是，XCTest不能总是很好地与轮式选择器控件(PickerWheel)进行交互。有时，setValue()方法调用可能没有任何效果。

如何让XCTest更好地兼容轮式选择器：
- 如果轮式选择器视图很简单，例如只包含文本内容：月份，日期偶国家名称。这种情况下 setValue()方法可以生效。
- 如果轮式选择器视图比较复杂，例如包含了国旗图像和国家名称组合，这种情况下失败的概率就很大了。


### 单个轮式选择器(PickerWheel)

```java
String txt = "exact_text";
MobileElement el = (MobileElement) driver.findElement(MobileBy.className("XCUIElementTypePickerWheel"));
el.setValue(txt);
```

### 多个轮式选择器(PickerWheel)

```java
String txt = "exact_text";
List<MobileElement> el = driver.findElements(MobileBy.className("XCUIElementTypePickerWheel"));

// set first PickerWheel
el.get(0).setValue(txt);

// set second PickerWheel
el.get(1).setValue(txt);
```

