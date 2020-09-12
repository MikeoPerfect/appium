## 新手入门

本文将会带你了解并运行一个简单的appium案例以及向你介绍一些关于appium的基本概念。想要了解更多关于appium的详细信息，请查看[相关介绍](/docs/cn/about-appium/intro.md)。

### 安装appium

Appium可以通过以下两种方式进行安装：使用[NPM](https://npmjs.com)命令或者是下载[appium客户端](https://github.com/appium/appium-desktop)
，一种基于桌面图形化的方式来启动appium服务。

#### 使用NPM命令进行appium安装

如果你想使用`npm install`命令安装appium，或者是改造appium，或者提交代码为appium做贡献，你都需要安装[Node.js和NPM](http://nodejs.org)（使用[nvm](https://github.com/creationix/nvm),[n](https://github.com/visionmedia/n)命令，或者是`brew install node`命令来安装node.js。请确认你没有使用`sudo`命令进行Node或者Appium的安装，否则运行时会出现问题）尽管Appium支持Node10及以上版本，我们仍然推荐使用最新稳定版。

Appium的安装直接使用如下命令即可：
```
npm install -g appium
```

#### 通过下载桌面应用的方式来进行Appium的安装

可直接从[版本发行页面](https://github.com/appium/appium-desktop/releases)点击下载最新版的Appium桌面版。

### 指定系统的 driver安装

你可能想要用Appium来进行不同应用的自动化操作，例如iOS应用或者是Android应用，Appium driver 提供了对于不同平台的自动化操作。下面列举的driver类型可以使你在不同的平台都能使用自动化技术，并且每种driver都有他们特定的安装要求。对于某个平台来说，driver的安装要求与在该平台上进行app开发所需的环境要求大多一致。例如，如果你想使用任意一种Android driver来进行Android应用的自动化操作，那么你所使用的的系统中应该配置好Android SDK.

在某些情况下，对于你想进行自动化操作的平台，请确认你查看过对应driver的文档，以便能正确进行安装：
- [XCUITest driver](/docs/cn/drivers/ios-xcuitest.md) (iOS和tvOS应用使用)
- [Espresso driver](/docs/cn/drivers/android-espresso.md) (Android应用使用)
- [UiAutomator2 driver](/docs/cn/drivers/android-uiautomator2.md) (Android应用使用)
- [Windows driver](/docs/cn/drivers/windows.md) (Windows操作系统桌面应用使用)
- [Mac driver](/docs/cn/drivers/mac.md) (Mac操作系统桌面应用使用)

### 验证安装

你可以使用`appium-doctor`命令来确认安装Appium所需的依赖是否都已满足要求。使用`npm install -g appium-doctor`命令来进行上述命令的安装，安装完成后，运行`appium-doctor`命令确认Appium所需的依赖都已正确安装，该命令还支持与`--ios`或者 `--android`选项一起搭配使用。

### Appium 客户端

当上述所需条件都已满足，Appium 其实是一个HTTP服务器而已。它需要与客户端进行连接，并由客户端发出指令告诉它应该开启哪种会话，还有一旦会话启动成功后该进行哪些自动化操作。这就意味着你永远不能只单独使用Appium本身，你需要将它与某一个客户端一起搭配使用（或者，如果你具有探索精神，可以使用cURL的方式进行尝试）

幸运的是，Appium与[Selenium](http://www.seleniumhq.org/)使用同一种协议，称为WebDriver协议。也许在你使用的系统中已经安装了多个客户端，但你只需要搭配任意一种标准Selenium客户端便足够运行Appium进行多种操作，特别是当你使用Appium来进行移动平台上的浏览器测试的时候。

尽管如此，正如移动端可以进行的某些操作不能在浏览器端进行，有些操作也是Appium可以但是Selenium却不行。因此，为了弥补这些不足，我们在传统Selenium客户端已有功能的基础上进行了相应的扩展，提供了一系列支持不同编程语言的Appium客户端。你可通过查看[Appium客户端列表](/docs/cn/about-appium/appium-clients.md)页面，点击相应的链接进行下载。

在进行下一步之前，请确认你已经根据自己使用的语言类型下载好了对应的客户端并准备好一切所需条件

### 启动Appium

现在我们可以打开Appium服务端，通过使用下面的命令行进行Appium的启动（假设NPM命令已经安装成功）：

```
appium
```

或者是点击Appium客户端页面上比较显眼的启动按钮。

Appium启动成功后将会向你展示一段简短的欢迎消息，其中包含了你目前所使用的Appium版本号和正在监听的端口号（默认使用`4723`）。该监听端口信息很重要，因为你需要确认测试客户端能通过该端口号顺利连接上Appium。如果你想要修改默认端口号，你可以在启动Appium时通过使用`-p`选项进行端口的设置（请确认已经查看过完整的[服务端参数列表](/docs/cn/writing-running-appium/server-args.md)文档）

### 运行你的第一个测试用例

在该部分，我们将会运行一个简单的“Hello World”Android测试用例。之所以选择Android是因为它在所有平台上都能运行。同时，我们将使用[UiAutomator2 driver](/docs/cn/drivers/android-uiautomator2.md)，所以请确保你已经通读过相关文档并且系统已经具备所需的环境。本次将使用JavaScript作为开发语言，以便于不需要再使用到其他的依赖组件。

（有可能你最终想进行自动化测试的平台并非Android，使用的编程语言也并非JavaScript。对于这种情况，可以查看[代码示例](https://github.com/appium/appium/tree/master/sample-code)文档, 其中包含了不同编程语言及运行平台的代码示例。）
）
#### 前提条件

- 我们假设你已经配置好并能成功运行Android8.0模拟器（在低版本上运行该示例时，修改对应的版本号即可）
- 我们假设你已经将所需的[测试APK](https://github.com/appium/appium/raw/master/sample-code/apps/ApiDemos-debug.apk)下载到本地系统

#### 配置 Appium 客户端

在本次示例中，我们将使用[Webdriver.io](http://webdriver.io)作为我们的Appium客户端。首先为该示例代码创建一个目录，然后运行下面的命令：

```
npm init -y
```
一旦项目初始化成功，则接下来就可以使用下面的命令进行`webdriverio`的安装：
```
npm install webdriverio
```

#### 初始化会话

现在我们可以创建一个名为`index.js`的测试文件，并且进行客户端的初始化：

```js
// javascript
const wdio = require("webdriverio");
```

接下来我们需要做的是启动一个Appium会话。通过定义一系列的服务选项和参数配置，并使用`wdio.remote()`方法来进行调用。这里所讲的参数配置其实仅仅是一些在会话初始化之后，发送至Appium服务端，告诉Appium我们想要进行哪些自动化操作的键值对。
对于任意Appium driver来说，至少应该包含以下这几个配置：
- `platformName`: 需要进行自动化操作的平台名称 
- `platformVersion`: 需要进行自动化操作的平台版本
- `deviceName`: 需要进行自动化的设备
- `app`: 需要进行自动化的APP路径 (与之相反，在进行浏览器自动化操作的时候需要使用`browserName`设置项)
- `automationName`: 需要使用的驱动名称

更多关于配置项和Appium中可用的配置项列表信息，可查看[参数配置文档](/docs/cn/writing-running-appium/caps.md).

下面所示测试文件中的代码向我们展示了怎样进行会话的开启：

```js
// javascript
const opts = {
  path: '/wd/hub',
  port: 4723,
  capabilities: {
    platformName: "Android",
    platformVersion: "8",
    deviceName: "Android Emulator",
    app: "/path/to/the/downloaded/ApiDemos.apk",
    appPackage: "io.appium.android.apis",
    appActivity: ".view.TextFields",
    automationName: "UiAutomator2"
  }
};

async function main () {
  const client = await wdio.remote(opts);

  await client.deleteSession();
}

main();
```

#### 运行测试命令

上一个步骤中我们已经将Appium的端口进行了设置，也根据自己的需求进行了参数配置（但是不要忘记将代码中的APK路径更换为自己系统中的实际路径）
并且使用`webdriverio`将上述配置进行了注册，现在我们已经创建好了能与Appium服务器进行连接的客户端对象。至此，我们可以继续后续的启动会话，
执行一些测试命令和关闭会话等操作。在本次测试中，我们将会执行一个简单的文本框输入操作并检查输入的文本是否正确。

```js
// javascript

const field = await client.$("android.widget.EditText");
await field.setValue("Hello World!");
const value = await field.getText();
assert.equal(value, "Hello World!");
```

当我们创建好了会话并且登录了应用后，接下来需要做的就是利用Appium在应用的层次结构中找到所需的元素并进行输入操作。
然后查询该元素并获取其文本内容，获取到的内容应该与断言中的期望值一致。

将上述所有代码整合在一起，完整的文件内容如下所示：

```js
// javascript

const wdio = require("webdriverio");
const assert = require("assert");

const opts = {
  path: '/wd/hub',
  port: 4723,
  capabilities: {
    platformName: "Android",
    platformVersion: "8",
    deviceName: "Android Emulator",
    app: "/path/to/the/downloaded/ApiDemos.apk",
    appPackage: "io.appium.android.apis",
    appActivity: ".view.TextFields",
    automationName: "UiAutomator2"
  }
};

async function main () {
  const client = await wdio.remote(opts);

  const field = await client.$("android.widget.EditText");
  await field.setValue("Hello World!");
  const value = await field.getText();
  assert.equal(value,"Hello World!");

  await client.deleteSession();
}

main();
```

你可以尝试自己运行这个示例。只需要将上述代码保存并且使用下面的命令执行即可。

`node`:
```
node index.js
```

如果一切顺利，你将会看到Appium开始产生日志，最终屏幕上会弹出应用并且开始进行操作仿佛有一个无形的用户在进行点击

### 接下来的内容

上述内容中我们只是接触到了一些Appium的皮毛。查看下面所示文档更好的帮助你进行Appium的使用

- [命令相关](https://appium.io/docs/cn/commands/status/) - 学习可用的命令，如何将它们与特定的客户端进行使用等...
- [代码示范目录](https://github.com/appium/appium/tree/master/sample-code) 可查看多种代码示例
- [Appium论坛](https://discuss.appium.io) - 这是一个可以更好的帮助你进行入门学习，或者是当你遇到困难时可以寻求帮助的Appium社区论坛
- [问题追踪](https://github.com/appium/appium/issues) - 如果你认为自己发现了问题，可通过此方式让Appium维护者知晓
