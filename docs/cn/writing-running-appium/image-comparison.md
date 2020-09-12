# 图片对比功能
本篇描述Appium支持的图片对比的一系列功能。这些功能依赖OpenCV 3动态库，图片对比在所有的driver中都可以调用。并且，每个功能都可以可视化展示对比结果，所以你可以通过跟踪不同参数的执行结果，对比得到最好的一个。

## 前置条件
- OpenCV 3+ 的本地库文件
- 安装npm [opencv4nodejs](https://github.com/justadudewhohacks/opencv4nodejs) 模块: `npm i -g opencv4nodejs`. 安装 opencv4nodejs 默认会从源下载所需的OpenCV有关的库文件，但是需要本地的开发工具能够访问到它们。
- Appium Server 1.8.0+


## 目的
图片对比方便运用在许多自动化的任务中，比如：
- 判定给出的图片当前是否在屏幕上
- 计算重新定义过的屏幕对象的坐标值
- 判定当前屏幕对象的状态是否是期望的状态

## 基于特征的对比
通过模板来执行图片对比，能够在整图中找出部分图片出现的可能性。关于该主题，可参考 https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_feature2d/py_matcher/py_matcher.html 。这类对比通常在判断原图是否被旋转/缩放的场景下很有用处。

### 代码示例
```java
// java

byte[] screenshot = Base64.encodeBase64(driver.getScreenshotAs(OutputType.BYTES));
FeaturesMatchingResult result = driver
        .matchImagesFeatures(screenshot, originalImg, new FeaturesMatchingOptions()
                .withDetectorName(FeatureDetector.ORB)
                .withGoodMatchesFactor(40)
                .withMatchFunc(MatchingFunction.BRUTE_FORCE_HAMMING)
                .withEnabledVisualization());
assertThat(result.getVisualization().length, is(greaterThan(0)));
assertThat(result.getCount(), is(greaterThan(0)));
assertThat(result.getTotalCount(), is(greaterThan(0)));
assertFalse(result.getPoints1().isEmpty());
assertNotNull(result.getRect1());
assertFalse(result.getPoints2().isEmpty());
assertNotNull(result.getRect2());
```

示例代码中`FeaturesMatchingOptions`类方法的使用具体细节包含在源码的doc描述当中（译者注：下载源码即可查看）。

```ruby
# Ruby
image1 = File.read 'first/image/path.png'
image2 = File.read 'second/image/path.png'

match_result = @driver.match_images_features first_image: image1, second_image: image2
assert_equal %w(points1 rect1 points2 rect2 totalCount count), match_result.keys

match_result_visual = @driver.match_images_features first_image: image1, second_image: image2, visualize: true
assert_equal %w(points1 rect1 points2 rect2 totalCount count visualization), match_result_visual.keys
File.open('match_result_visual.png', 'wb') { |f| f<< Base64.decode64(match_result_visual['visualization']) }
assert File.size? 'match_result_visual.png'
```

### 可视化示例
![基于特征的对比示例](https://user-images.githubusercontent.com/7767781/38800997-f7408fb8-4168-11e8-93b9-cfe3d51ecf1c.png)


## 图片存在查询
通过模板执行整图匹配，查找局部图片存在概率相关的主题的细节，可参考阅读 https://docs.opencv.org/2.4/doc/tutorials/imgproc/histograms/template_matching/template_matching.html 的内容。如果部分图像是完整图像一部分，这类比较就非常适用。

查询图片存在和基于特征的图片对比之间存在细微的差别。当要查找的图像是目标/屏幕截图的子集时，使用前者。当要找到的图像与目标基本相同，但旋转或缩放时，使用后者。

### 代码示例
```java
// java
byte[] screenshot = Base64.encodeBase64(driver.getScreenshotAs(OutputType.BYTES));
OccurrenceMatchingResult result = driver
        .findImageOccurrence(screenshot, partialImage, new OccurrenceMatchingOptions()
                .withEnabledVisualization());
assertThat(result.getVisualization().length, is(greaterThan(0)));
assertNotNull(result.getRect());
```

示例代码中`OccurrenceMatchingOptions`类方法的使用具体细节包含在源码的doc描述当中（译者注：下载源码即可查看）。

```ruby
# Ruby
image1 = File.read 'first/image/path.png'
image2 = File.read 'partial/image/path.png'

find_result = @driver.find_image_occurrence full_image: image1, partial_image: image2
assert_equal({ 'rect' => { 'x' => 0, 'y' => 0, 'width' => 750, 'height' => 1334 } }, find_result)

find_result_visual = @driver.find_image_occurrence full_image: image1, partial_image: image2, visualize: true
assert_equal %w(rect visualization), find_result_visual.keys
File.open('find_result_visual.png', 'wb') { |f| f<< Base64.decode64(find_result_visual['visualization']) }
assert File.size? 'find_result_visual.png'
```

```javascript
// Typescript / Javascript
  /*
     Typescsript code for occurrence comparison using the template matching algorithm.
     It detects if an image is contained in another image (called the template).
     The image must have the same scale and look the same. However, you can add a scaling transformation beforehand.

     official doc:
     https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/image-comparison.md
     OpenCV algorithm doc:
     https://docs.opencv.org/2.4/doc/tutorials/imgproc/histograms/template_matching/template_matching.html
     official sample code:
     https://github.com/justadudewhohacks/opencv4nodejs/blob/master/examples/templateMatching.js

     You must install opencv4nodejs using the -g option.

     The Javascript client driver webdriverio does not support (in January 2020) the "-image" strategy implemented in the Appium server. You will have more power and understanding while using openCV directly. Since the appium server is in Javascript, you can do all it does with opencv in your test suite.

     The testing framework mocha can be run with typescript to have async/await.
     You need to run mocha with those options in the right order and with the associated packages installed:
     NODE_PATH=/path/to/nodejs/lig/node_modules TS_NODE_PROJECT=config/tsconfig_test.json --require ts-node/register --require tsconfig-paths/register
     You will also need to make a basic config/tsconfig_test.json
     Note that paths in tsconfig.json does not support absolute paths. Hence, you cannot move the NODE_PATH there.
  */
  import * as path from 'path';
  const cv = require(path.join(process.env.NODE_PATH, 'opencv4nodejs'));
  const isImagePresent = async () => {
    /// Take screenshot and read the image
    const screenImagePath = './appium_screenshot1.png';
    await driver.saveScreenshot(screenImagePath)
    const likedImagePath = './occurrence1.png';

    // Load images
    const originalMatPromise = cv.imreadAsync(screenImagePath);
    const waldoMatPromise = cv.imreadAsync(likedImagePath);
    const [originalMat, waldoMat] = await Promise.all([originalMatPromise, waldoMatPromise]);

    // Match template (the brightest locations indicate the highest match)
    // In the OpenCV doc, the option 5 refers to the algorithm called CV_TM_CCOEFF_NORMED
    const matched = originalMat.matchTemplate(waldoMat, 5);

    // Use minMaxLoc to locate the highest value (or lower, depending of the type of matching method)
    const minMax = matched.minMaxLoc();
    const { maxLoc: { x, y } } = minMax;

    // Draw bounding rectangle
    originalMat.drawRectangle(
      new cv.Rect(x, y, waldoMat.cols, waldoMat.rows),
      new cv.Vec(0, 255, 0),
      2,
      cv.LINE_8
    );

    // Open result in new window
    // If the image is too big for your screen, you need to write to a file instead.
    // Check the source of opencv4nodejs for writing an image to a file.
    cv.imshow('We\'ve found Waldo!', originalMat);
    await cv.waitKey();

    // then you know if the image was found by comparing the rectangle with a reference rectangle.
    // the structure minMax contains the property maxVal that gives the quality of the match
    // 1 is prefect match, but you may get .999. If you extract an image from the screenshot manually,
    // you will get an image that matches.
  };
```

### 可视化示例
![图片存在查询](https://user-images.githubusercontent.com/7767781/40233298-b7decfe4-5aa2-11e8-8c9b-f85f384d2092.png)


左下角突出显示的图片![Waldo](https://github.com/appium/appium-support/blob/master/test/images/waldo.jpg?raw=true)是查找的结果匹配。


## 相似度计算
图片相似度是通过计算图片之间相似性的分数来执行的。对比过程类似于图片存在查询中用到的`findImageOccurrence`，但是必须保证的是两个图像的大小要相等。如果原始图像是原始图像的副本，但内容发生了更改，这类比较就非常适用。

### 代码示例
```java
// java

byte[] screenshot1 = Base64.encodeBase64(driver.getScreenshotAs(OutputType.BYTES));
byte[] screenshot2 = Base64.encodeBase64(driver.getScreenshotAs(OutputType.BYTES));
SimilarityMatchingResult result = driver
        .getImagesSimilarity(screenshot1, screenshot2, new SimilarityMatchingOptions()
                .withEnabledVisualization());
assertThat(result.getVisualization().length, is(greaterThan(0)));
assertThat(result.getScore(), is(greaterThan(0.0)));
```

示例代码中`SimilarityMatchingOptions`类方法的使用具体细节包含在源码的doc描述当中（译者注：下载源码即可查看）。


```ruby
# Ruby
image1 = File.read 'first/image/path.png'
image2 = File.read 'second/image/path.png'

get_images_result = @driver.get_images_similarity first_image: image1, second_image: image2
assert_equal({ 'score' => 0.891606867313385 }, get_images_result)

get_images_result_visual = @driver.get_images_similarity first_image: image1, second_image: image2, visualize: true
assert_equal %w(score visualization), get_images_result_visual.keys
File.open('get_images_result_visual.png', 'wb') { |f| f<< Base64.decode64(get_images_result_visual['visualization']) }
assert File.size? 'get_images_result_visual.png'
```

### Visualization Example
### 可视化示例
![相似度计算示例](https://user-images.githubusercontent.com/7767781/38780635-27198346-40da-11e8-803d-1ec4afd3c3aa.png)

两张图片的相似度得分在0.98以上。
