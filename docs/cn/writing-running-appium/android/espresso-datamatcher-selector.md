## Espresso DataMatcher选择器

通过委托给Espresso的[Data Matcher](https://developer.android.com/reference/android/support/test/espresso/DataInteraction)，我们可以定位在视口中不可见的视图，而无需手动滚动屏幕上的视图。

### 适配器视图

Android应用程序有特殊类型的[AdapterViews](https://developer.android.com/reference/android/widget/AdapterView)视图（如：`ScrollView`，`ListView`，`GridView`），但其只渲染那些屏幕上可见的子视图。AdapterView具有“adapter”对象，该对象存储该视图子级的所有数据，包括未呈现的视图。

使用Espresso的数据匹配器时，您可以编写一个[Hamcrest matcher](http://hamcrest.org/JavaHamcrest/javadoc/1.3/org/hamcrest/Matchers.html)以从适配器中选择一个项，从而定位屏幕外的视图。如果该项不在视图层次结构中，则Espresso会自动将其滚动到视图中。

### 示例

这是从Android应用程序的源XML中获取的ListView：

```xml
<android.widget.ListView index="0" package="io.appium.android.apis" class="android.widget.ListView" checkable="false" checked="false" clickable="true" enabled="true" focusable="true" focused="false" scrollable="true" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,210][1080,1794]" resource-id="android:id/list" adapter-type="HashMap" adapters="{contentDescription=Animation, title=Animation, intent=Intent { cmp=io.appium.android.apis/.ApiDemos (has extras) }},{contentDescription=Auto Complete, title=Auto Complete, intent=Intent { cmp=io.appium.android.apis/.ApiDemos (has extras) }}, ...}">
    <android.widget.TextView index="0" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Drag and Drop" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,148][1080,274]" text="Drag and Drop" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="1" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Expandable Lists" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,277][1080,403]" text="Expandable Lists" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="2" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Focus" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,406][1080,532]" text="Focus" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="3" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Gallery" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,535][1080,661]" text="Gallery" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="4" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Game Controller Input" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,664][1080,790]" text="Game Controller Input" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="5" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Grid" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,793][1080,919]" text="Grid" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="6" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Hover Events" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,922][1080,1048]" text="Hover Events" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="7" package="io.appium.android.apis" class="android.widget.TextView" content-desc="ImageButton" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1051][1080,1177]" text="ImageButton" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="8" package="io.appium.android.apis" class="android.widget.TextView" content-desc="ImageSwitcher" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1180][1080,1306]" text="ImageSwitcher" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="9" package="io.appium.android.apis" class="android.widget.TextView" content-desc="ImageView" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1309][1080,1435]" text="ImageView" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="10" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Layout Animation" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1438][1080,1564]" text="Layout Animation" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="11" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Layouts" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1567][1080,1693]" text="Layouts" hint="false" resource-id="android:id/text1" />
    <android.widget.TextView index="12" package="io.appium.android.apis" class="android.widget.TextView" content-desc="Lists" checkable="false" checked="false" clickable="false" enabled="true" focusable="false" focused="false" scrollable="false" long-clickable="false" password="false" selected="false" visible="true" bounds="[0,1696][1080,1822]" text="Lists" hint="false" resource-id="android:id/text1" />
</android.widget.ListView>
```

这ListView控件显示菜单项[ `Drag and Drop`，`Expandable Lists`...直到`Lists`]。此菜单还有其他几个不在屏幕上的项，无法使用标准定位器定位。例如，有一个名为`TextClock`的菜单项在View层次结构中不可见。

`ListView`上面的XML中的节点具有一个名为的属性`adapters`，其中包含“备份” ListView的数据：

```js
{
    contentDescription = Animation, title = Animation, intent = Intent {
        cmp = io.appium.android.apis / .ApiDemos(has extras)
    }
}, {
    contentDescription = Auto Complete,
    title = Auto Complete,
    intent = Intent {
        cmp = io.appium.android.apis / .ApiDemos(has extras)
    }
}, {
    contentDescription = Buttons,
    title = Buttons,
    intent = Intent {
        cmp = io.appium.android.apis / .view.Buttons1
    }
},
...
```

这些项可以使用数据匹配器选择器来定位。以下为显示如何找到并单击`TextClock`的代码段：

```js
// Javascript example
driver.findElementById("list")
  .findElement("-android datamatcher", JSON.stringify({
    "name": "hasEntry",
    "args": ["title", "TextClock"]
  }))
  .click();
```

```ruby
# Ruby
@driver.find_element(:id, 'list')
  .find_element(:data_matcher, {
    name: 'hasEntry',
    args: ['title', 'TextClock']
  }.to_json)
  .click
```

```python
# Python
driver.find_element_by_id('list')
    .find_element_by_android_data_matcher({
        name='hasEntry',
        args=['title', 'TextClock']
    })
    .click()
```

此Appium选择器等效于在Espresso中编写此匹配器：

```java
// Espresso code (not Appium code)
onData(hasEntry("title", "textClock")
  .inAdapterView(withId("android:id/list))
  .perform(click());
```

在此示例中，我们使用ID选择器选择父对象`AdapterView`，然后通过应用与对象`title="TextClock"`匹配的Hamcrest Matcher找到该视图的子对象。

`AdapterView`如果“活动”只有一个适配器视图，则无需定位父对象。在这种情况下，可以将其省略。

```js
driver.findElement("-android datamatcher", JSON.stringify({
    "name": "hasEntry",
    "args": ["title", "TextClock"]
  }))
  .click();
```

```ruby
# Ruby
@driver.find_element(:data_matcher, {
  name: 'hasEntry',
  args: ['title', 'TextClock']
}.to_json).click
```

```python
# Python
driver.find_element_by_android_data_matcher({
    name='hasEntry',
    args=['title', 'TextClock']
}).click()
```

### 编写选择器

数据匹配器选择器使用Java reflection来调用用于定位适配器对象的[Hamcrest匹配器](http://hamcrest.org/JavaHamcrest/javadoc/1.3/org/hamcrest/Matchers.html)。匹配器为JSON格式，并且具有此格式

```js
{
  "name": "<METHOD_NAME>",
  "args": [...],
```

该名称是Hamcrest匹配器方法名称。默认为`org.hamcrest.Matchers`名称空间，但是也可以使用匹配器方法全称（例如：`android.support.test.espresso.matcher.CursorMatchers.withRowBlob`）。

args是该方法采用的参数列表（如果不采用args则可以不确定）。这些可以是字符串，数字，布尔值或其他JSON定义的Hamcrest Matcher。

### JSON匹配器样本

具有等效Espresso`onData`匹配器的JSON匹配器示例

#### 开头

```js
// 'startsWith' JSON
{
  "name": "startsWith",
  "args": "substr" // if it's a single arg, we don't need args to be an array
}
```

```java
// Espresso 'startsWith' example
onData(startsWith("substr"));
```

#### 多个匹配器

```js
// 'multiple matchers' JSON
{
  "name": "allOf",
  "args": [
    {"name": "instanceOf", "args": "Map.class"},
    {"name": "hasEntry", "args": {
      "name": "equalTo", "args": "STR"
    }},
    {"name": "is", "args": "item: 50"}
  ]
}
```

```java
// Espresso 'multiple matchers' example
onData(allOf(is(instanceOf(Map.class)), hasEntry(equalTo("STR"), is("item: 50"))));
```

#### Cursor匹配器

```js
// 'cursor matchers' JSON
{
  "name": "is", "args": {
    "name": "instanceOf", "args": "Cursor.class"
  },
  "name": "CursorMatchers.withRowString", "args": [
    "job_title", {"name": "is", "args": "Barista"}
  ]
}
```

```java
// Espresso 'cursor matchers' example
onData(
    is(instanceOf(Cursor.class)),
    CursorMatchers.withRowString("job_title", is("Barista"))
);
```


### 资源

- [Espresso中的视图与数据说明](https://medium.com/androiddevelopers/adapterviews-and-espresso-f4172aa853cf)
- [Espresso清单](https://developer.android.com/training/testing/espresso/lists)

