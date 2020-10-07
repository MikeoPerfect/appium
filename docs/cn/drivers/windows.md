# Windows驱动程序
---

Appium支持自动运行Windows PC桌面应用程序，该驱动程序依赖于微软的项目[WinAppDriver](https://github.com/Microsoft/WinAppDriver)。WinAppDriver是一个与appium兼容的WebDriver服务器， 适用于Windows桌面应用程序，
通常缩写为WAD。WAD通常与Appium捆绑在一起安装，不需要单独安装。

Windows驱动程序支持测试通用Windows平台(UWP)和经典Windows(Win32)应用程序。

除了WAD存储库，Appium也在[appium-windows-driver](https://github.com/appium/appium-windows-driver)存储库中进行开发。


## 需求和支持
（除了Appium的一般要求外）
* 装有Windows 10或更高版本的Windows PC
* 支持进入管理员模式

## 使用
使用Windows驱动程序启动回话的方法：
* 确保在[新的会话请求](https://github.com/JiangSine/appium/blob/master/docs/cn/drivers/windows.md#TODO)中包含platformName[功能](https://github.com/JiangSine/appium/blob/master/docs/cn/drivers/windows.md#TODO)且值为Windows
* 确保deviceName功能设置为WindowsPC
* 至少包括适当的应用程序功能（请参阅下文）

## 功能
Windows驱动程序支持许多标准的[Appium功能](https://github.com/JiangSine/appium/blob/master/docs/cn/writing-running-appium/caps.md)。请参阅下面的内容，了解如何将他们专门用于Windows驱动程序。

### 设置
确保打开[开发人员模式](https://docs.microsoft.com/en-us/windows/uwp/get-started/enable-your-device-for-development)即可进行Windows应用测试。

在运行Appium时，无论是通过Appium Desktop启动还是命令行启动，请确保以管理员身份进行操作。

### 为Windows驱动程序编写测试脚本
您可以参照现有示例：

#### Java样本
1. 在Java IDE(例如IntelliJ)中，将示例文件夹作为现有项目打开。例如：[CalculatorTest](https://github.com/Microsoft/WinAppDriver/tree/master/Samples/Java/CalculatorTest).
2. 在Java IDE中构建并运行测试。

#### C#示例
1. 在[CalculatorTest](https://github.com/Microsoft/WinAppDriver/tree/master/Samples/C%23/CalculatorTest)文件下拉出并打开CalculatorTest.sln
2. 在带有测试解决方案的Visual Studio 2015中打开构建测试，选择测试->运行->所有测试。

#### JavaScript/node示例
1. 使用selenium-webdriver

[Examples on selenium-appium](https://github.com/react-native-windows/selenium-appium/tree/master/example)

[selenium-webdriver-winappdriver-example](selenium-webdriver-winappdriver-example)

如果您想从头开始编写测试，则可以选择Appium/Selenium支持的任何编程语言或工具来编写测试脚本。 在下面的示例中，我们将使用Microsoft Visual Studio 2015在C＃中编写测试脚本。

#### 创建测试项目

1. 打开Microsoft Visual Studio 2015
2. 创建测试项目和解决方案。 选择“新建项目”>“模板”>“ Visual C＃”>“测试”>“单元测试项目”
3. 创建完成后，选择“项目”>“管理NuGet程序包...”>浏览并搜索Appium.WebDriver
4. 为测试项目安装Appium.WebDriver NuGet软件包
5. 开始编写测试（请参阅[示例]下的示例代码）

#### 通用Windows平台应用程序测试
要测试UWP应用，您可以使用任何Selenium支持的语言，只需在应用功能条目中指定被测试应用的ID。 以下是使用C＃编写的案例，针对Windows Alarms＆Clock应用程序创建测试会话的示例：

```
	// Launch the AlarmClock app
	DesiredCapabilities appCapabilities = new DesiredCapabilities();
	appCapabilities.SetCapability("app", "Microsoft.WindowsAlarms_8wekyb3d8bbwe!App");
	AlarmClockSession = new WindowsDriver<WindowsElement>(new Uri("http://127.0.0.1:4723"), appCapabilities);
	// Control the AlarmClock app
	AlarmClockSession.FindElementByAccessibilityId("AddAlarmButton").Click();
	AlarmClockSession.FindElementByAccessibilityId("AlarmNameTextBox").Clear();
```

 测试自己编写的应用程序时，可以在生成的AppX\\vs.appxrecipe文件中找到应用程序ID,如下：

`RegisteredUserNmodeAppID` node. E.g. `c24c8163-548e-4b84-a466-530178fc0580_scyf5npe3hv32!App`

#### 经典Windows App测试
要测试经典Windows应用程序，可以使用任何Selenium支持的语言，并在应用程序功能条目中指定被测应用程序的完整可执行路径。 以下是为Windows记事本应用程序创建测试会话的示例：

```
	// Launch Notepad
	DesiredCapabilities appCapabilities = new DesiredCapabilities();
	appCapabilities.SetCapability("app", @"C:\Windows\System32\notepad.exe");
	NotepadSession = new WindowsDriver<WindowsElement>(new Uri("http://127.0.0.1:4723"), appCapabilities);
	// Control the AlarmClock app
```

#### 开始会话
如上所述，请使用以下功能来确保获得Windows App自动化会话：

`platformName：Windows deviceName：WindowsPC app：`用于测试的Windows应用程序的appID，或.exe文件的路径

#### 检查UI元素
默认情况下，Microsoft Visual Studio 2015包括Windows SDK，该SDK提供了很好的工具来检查您正在测试的应用程序。 通过该工具，您可以使用Windows应用程序驱动程序查询的每个UI元素/节点。 可以在Windows SDK文件夹（例如C：\\Program Files（x86）\\Windows Kits\\10\\bin\\x86）下找到inspect.exe工具。 该工具将显示各种元素属性。 下表显示了应使用哪种Appium定位器策略来查找具有相应属性的元素。

| 定位策略          | 匹配属性         |
| :---             | :---            |
| accessibility id | AutomationId    |
| class name       | ClassName       |
| name             | Name            |
