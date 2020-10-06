# 安全

Appium团队在尽一切努力提高Appium 服务端的安全性。尤其在多租户环境或多个用户在同一个服务端上运行会话时，安全性尤为必要。一般来说，如果您在本地运行自己的Appium服务，而且不会和其他人共享它，或者将服务暴露在互联网上，那么可以不用担心安全问题，您可以放心大胆的启用Appium所有的功能。

但是，鉴于很多Appium的用户可能无法保证有一个安全的运行环境，Appium团队将许多功能后置于安全保护机制之后，强制系统管理员（负责启动Appium服务的家伙）显示的选择启用这些置于安全机制之后的功能。

出于安全考虑，Appium的客户端会话不能通过设置capabilities，以发送请求的方式来开启那些（启用了安全机制的）功能。这属于启动Appium服务器那个家伙的责任。

## 安全相关的服务启动参数
[server-args](/docs/cn/writing-running-appium/server-args.md)文档概述了从命令行启动Appium可以传递的三个相关参数：

* `--relaxed-security`:设置该项会开启所有非安全功能（`--deny-insecure`没有设置为的情况下；参考下方描述）
* `--allow-insecure`：该项设置启用给定的功能列，它跟的参数是逗号分隔符的功能列表，或者是一个包含功能列表（一个功能占一行）的文件路径。比如：`--allow-insecure=adb_shell`的设置仅会开启adb shell的功能。该设置是可以生效的，但结合设置`--relaxed-security`参数（启用所有功能的设置）就没有意义了。
* `--deny-insecure`：该项设置同样可以传入给定的功能列或者是一个包含功能列表（一个功能占一行）的文件路径。不管是设置了`--relaxed-security` ，还是设置了`--allow-insecure`，`--deny-insecure`列出的任何功能都将被禁用。

## 不安全的功能

每个Appium驱动程序负责其自身的安全性，并可以创建自己的功能名称。下表是我们所知道的Appium驱动程序官方支持的的功能和名称。
|特性名称|描述|AutomationName|
|------------|-----------|-------|
|`get_server_logs`|允许通过Webdriver日志接口检索Appium服务器日志|IOS, XCUITest, Android, UiAutomator2, Espresso|
|`adb_shell`|允许通过ADB命令执行任意的`mobile: shell`命令。|Android, UiAutomator2, Espresso|
|`shutdown_other_sims`|允许任何会话使用capability来关闭任何服务器上正在运行的模拟器|XCUITest|
|`perf_record`|允许记录系统性能和其他的模拟器指标|XCUITest|
|`record_audio`|允许记录主机的音频输入|XCUITest|
|`chromedriver_autodownload`|允许自动下载适当的ChromeDriver版本 |Android, UiAutomator2, Espresso|
|`execute_driver_script`| 允许发送包含多个Appium命令参数的请求。参考阅读 [文档](https://github.com/appium/appium/blob/master/docs/cn/commands/session/execute-driver.md) 获得更多细节|All|

也可以参考下面的链接，它们可能包含额外的设置项。

- [appium-android-driver](https://github.com/appium/appium-android-driver#opt-in-features-with-security-risk)
- [appium-xcuitest-driver](https://github.com/appium/appium-xcuitest-driver#opt-in-features-with-security-risk)
- [appium-mac-driver](https://github.com/appium/appium-mac-driver#opt-in-features-with-security-risk)

## 写给Driver的开发者
两个方法存在于扩展了`BaseDriver`的类当中，使得在检查不安全功能的可用性时，Driver程序的开发人员的工作更加轻松：
* `this.isFeatureEnabled(name)`: 返回 true或false，取决于服务端安全设置的组合是否允许启用有问题的功能。
* `this.ensureFeatureEnabled(name)`: 如果有问题的功能不被允许使用，会抛出一个包含有功能名称和执行本文地址的错误。
