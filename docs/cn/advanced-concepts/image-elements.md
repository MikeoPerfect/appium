## 寻找图像元素并与之交互

使用实验性的 `-image` 定位器策略，可以给Appium发送一个代表你想点击的元素的图片文件。如果Appium能找到一个与你的模板相匹配的屏幕区域，它将把这个区域的信息包装成一个标准的 `WebElement`，并把它发回给你的Appium客户端。


该策略将为每个Appium客户端提供不同的方法，例如：`driver.findElementByImage()`。

### 图像选择器

结合任何定位器策略，你需要使用一个"选择器"来详细说明你的查找请求的具体性质。在 `-image` 策略的情况下，选择器必须是一个字符串，它是一个代表你要使用的匹配模板的base64编码的图像文件。

### 图像元素

如果图片匹配成功，Appium会缓存匹配信息，并创建一个标准响应供你的客户端使用，从而在你的测试脚本中实例化一个标准元素对象。使用这个元素对象，你可以在"图像元素"上调用少量的方法，就像它是一个真正的`WebElement`一样：

* `click`
* `isDisplayed`
* `getSize`
* `getLocation`
* `getLocationInView`
* `getElementRect`
* `getAttribute`
    * 如果 `getMatchedImageResult` 为 `true`，`visual` 将返回匹配的图像作为base64数据
    * 从 Appium 1.18.0 开始，`score`以浮点数形式返回相似度分数，范围为`[0.0, 1.0]`。

这些动作在"图像元素"上是被支持的，因为它们是只涉及使用屏幕位置的动作。其他的动作(比如`sendKeys`)是不支持的，因为Appium基于你的模板图像所能知道的就是是否有一个屏幕区域在视觉上与之匹配--Appium没有办法将这些信息转化为特定于驱动程序的UI元素对象，而这对于其他动作的使用是必要的。

重要的是要记住这一点：图像元素并没有什么"魔力"--它们只是参考屏幕坐标，因此 "点击 "图像元素在内部不过是Appium在图像元素的屏幕边界中心点构造一个点击（事实上你可以告诉Appium使用哪种API来执行这个点击--见下文）。

### 相关设置

由于通过图像寻找元素依赖于图像分析软件与Appium的截图功能和你自己提供的参考图像相结合，我们提供了一些设置，帮助你调节这个功能，在某些情况下可能会加快匹配速度或使其更准确。

要访问这些设置，你应该使用Appium [设置API](/docs/en/advanced-concepts/settings.md)。这些是可用的设置。

|设置名称|说明|可能值|默认值|
|------------|-----------|---------------|-------------|
|imageMatchThreshold|OpenCV的匹配阈值，低于这个阈值就认为查找失败。基本上，可能性的范围是在0（意味着不使用阈值）和1（意味着参考图像必须是完全像素对像素的匹配）之间。中间的精确值没有绝对意义。例如，一个需要大幅调整参考图像大小的匹配会比其他情况下的匹配强度低。建议你先尝试默认设置，如果没有找到匹配元素，再逐步降低阈值。如果你匹配到了错误的元素，可以尝试增加阈值。| 0到1之间 |0.4|
|fixImageFindScreenshotDims|Appium知道屏幕尺寸，最终这些尺寸是决定在屏幕上点击的位置的相关尺寸。如果检索到的屏幕截图（通过Appium的本地方法，或外部来源）与屏幕尺寸不匹配，这个设置决定了Appium会调整屏幕截图的尺寸来匹配，确保在正确的坐标上找到匹配的元素。如果你知道这不是必要的，请关闭这个设置，Appium会放弃检查，可能会加快一些速度。|`true` 或 `false`|`true`|
|fixImageTemplateSize|如果一个参考图片/模板的尺寸大于要匹配的基础图片，OpenCV将不允许匹配该图片。可能发生的情况是，你发送的参考图片的尺寸比Appium检索的截图大。在这种情况下，匹配会自动失败。如果你把这个设置为 `true`，Appium会调整模板的大小，以确保它至少比截图的尺寸小。|`true` 或 `false`|`false`|
|fixImageTemplateScale| Appium在与OpenCV匹配之前，会调整基础图像的大小以适应其窗口大小。如果你把这个设置设置为 `true`，Appium就会把你发送的参考图像按同样的比例缩放，Appium就会把基础图像按比例缩放以适应窗口大小。例如iOS截图是`750×1334`像素的基础图片，窗口大小为`375×667`时，Appium将基础图像重新缩放为窗口大小，缩放比例为`0.5`。参考图像是基于屏幕截图尺寸，从来没有图像与窗口尺寸的比例。这个设置允许Appium用`0.5`来缩放参考图像。[appium-base-driver#306](https://github.com/appium/appium-base-driver/pull/306)| `true` 或 `false` | `false` |
|defaultImageTemplateScale| Appium默认不调整模板图片的大小(值为1.0)。虽然，存储缩放的模板图像可能有助于节省存储空间的大小。例如，一个人可以用270×32像素的模板图像来表示1080×126像素的区域(defaultImageTemplateScale的值被期望设置为4.0)。更多细节请参考[appium-base-driver#307](https://github.com/appium/appium-base-driver/pull/307)。|例如 `0.5`, `10.0`, `100`| `1.0` |
|checkForImageElementStaleness|可能发生的情况是，在你匹配了一个图像元素和你选择点击它之间，这个元素已经不存在了。Appium判断这一点的唯一方法就是在点选之前尝试重新匹配模板。正如你所期望的那样，如果重新匹配失败，你会得到一个`StaleElementException`。将这个选项转为`false`来跳过检查，可能会加快检查速度，但也有可能会遇到陈旧元素的问题，而没有一个异常让你知道你跳过了。|`true` 或 `false`|`true`|
|autoUpdateImageElementPosition|匹配的图像在找到它和你点击它之间可能会发生位置变化。和之前的设置一样，如果Appium在重新匹配中确定位置改变了，它可以自动调整位置。|`true` 或 `false`|`false`|
|imageElementTapStrategy|为了点击找到的图片元素，Appium必须使用其中一个触摸动作策略。可用的策略是W3C Actions API，或旧的MJSONWP TouchActions API。除非你使用的驱动因某些原因不支持W3C Actions API，否则请坚持使用默认策略。|`"w3cActions"` 或 `"touchActions"`|`"w3cActions"`|
|getMatchedImageResult| Appium不存储匹配的图像结果。虽然，将结果存储在内存中可能会有助于调试是否有哪个区域被find by image匹配。Appium会将[属性](http://appium.io/docs/en/commands/element/attributes/attribute/)API中的图像作为`visual`返回。 | `true` 或 `false` | `false` |

请注意，每个特定语言的Appium客户端可能会通过特殊的常量来提供这些设置，这些常量可能会与上面提到的确切设置名称略有不同。

### 调试

`getMatchedImageResult`可能有助于调试Appium是否能如期找到所提供的图片。如果`getMatchedImageResult`是`true`，`visual`属性会返回base64数据。

```ruby
# Ruby core
@driver.update_settings({ getMatchedImageResult: true })
el = @driver.find_element_by_image 'path/to/img.ong'
img_el.visual # 返回base64编码的字符串
```

```python
# Python
self.driver.update_settings({"getMatchedImageResult": True})
el = self.driver.find_element_by_image('path/to/img.ong')
el.get_attribute('visual') # 返回base64编码的字符串
```

参考: https://github.com/appium/appium-base-driver/pull/327
