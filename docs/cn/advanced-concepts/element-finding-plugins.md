## 元素查找插件

从1.9.2版本开始，Appium支持使用插件来辅助查找元素，通过使用 `-custom` 定位策略。 目前此功能为实验性功能。

### 用法

1. 安装基于Appium元素查找插件标准开发的第三方元素查找插件 (参见下文)。 (必须是Node模块，通过NPM安装或者本地安装)。插件可以安装在你系统上的任意位置，不过主要有三种方式：
    * 独立于Appium的目录 (通过在任意文件夹运行 `npm install <plugin>`)
    * 在Appium依赖树下 (通过在Appium根目录下运行`npm install <plugin>`)
    * 在系统上全局安装 (通过运行 `npm install -g <plugin>`)

    (当然，插件本身可能有安装和部署说明，在插件的文档中会有详细说明。)

2. 在你的测试中添加一个新的capability：`customFindModules`。 这个capability必须是一个对象，至少有一个键和一个值。键名为 "插件快捷键"，值为"插件引用"。 例如：

    ```
    {
        "customFindModules": {
            "plug": "my-element-finding-plugin"
        }
    }
    ```

    "plug"是快捷方式，而"my-element-finding-plugin"是引用。在你的测试代码中只需要使用快捷方式，可以是满足JSON键名条件的任意字符串。引用必须是插件的Node模块引用，而且Appium可以通过Node的[模块获取方法](https://medium.freecodecamp.org/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8)来[获取](https://nodejs.org/api/modules.html#modules_require)。

一旦使用上述capability来启动一个session，可以说插件（或者多个插件---多插件当然是支持的）已经被注册上了。你可以通过下面的步骤来使用已注册的插件查找元素：

1. 使用`-custom` 定位策略
2. 在你的选择器前加上`<快捷方式(shortcut)>:`

因此，对于上面例子中的插件，如果你想使用"foo"选择器来查找元素，可以这样写（在客户端代码中）：

```js
driver.findElement('-custom', 'plug:foo');
```

换句话说，使用`-custom`定位策略，并发送`foo`作为选择器，从而确保Appium知道应该使用`plug`插件来处理查找元素请求。

如果只有一个插件注册了，可以在选择器中省略插件快捷方式（因为Appium不会混淆你想使用哪个插件）：

```js
driver.findElement('-custom', 'foo');
```

目前并非所有的Appium客户端都很好地支持了`-custom`定位策略；查看客户端文档获取此策略的正确调用方式。 

### 开发插件

任何人都可以开发Appium元素查找插件。只需符合下列规则：

* 插件必须是一个Node模块，且有一个名为`find`的导出(export)
* 当被调用的时候返回元素对象列表（可以为空）

当Appium调用你的`find`方法时，它会传递下列参数：

* 一个`driver`对象实例，代表当前session（比如`XCUITestDriver`实例）
* 一个日志对象，可以写入Appium日志
* 选择器（字符串），用户传入用于查找元素
* 一个布尔值：是否查找多个元素（true）或（false）。注意你必须返回一个数组，不管用户是否要查找多个元素。传递这个标志位是为了针对不需要返回多个元素的查询进行优化。

这就是目前的全部内容! 具体示例可查看以下已知插件列表。


### 已知插件列表

* [Test.ai Classifier](https://github.com/testdotai/appium-classifier-plugin)
