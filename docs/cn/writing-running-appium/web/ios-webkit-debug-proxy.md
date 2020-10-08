## iOS WebKit 调试代理

借助 [ios_webkit_debug_proxy](https://github.com/google/ios-webkit-debug-proxy) ，Appium 可以在 iOS 真机上访问 webview。

### 安装

#### 使用 Homebrew

在终端执行以下命令使用 Homebrew 安装最新版本的 ios-webkit-debug-proxy：

``` center
 # 没有安装 brew 时才需要第一条命令。
 > ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
 > brew update
 > brew install ios-webkit-debug-proxy
```

#### 从源码构建 ios-webkit-debug-proxy

在你的 linux 设备上打开命令终端。你可以通过喜欢的搜索引擎查找如何打开终端的操作指南。

```shell
$ cd  ~
$ sudo apt-get install autoconf automake libusb-dev libusb-1.0-0-dev libplist-dev libplist++-dev usbmuxd libtool libimobiledevice-dev
$ git clone https://github.com/google/ios-webkit-debug-proxy.git
$ cd ios-webkit-debug-proxy
$ ./autogen.sh
$ make
$ sudo make install
```


#### 运行 ios-webkit-debug-proxy

安装后使用以下命令启动代理：

``` 
# 修改 udid 为目标设备的 udid 并确认 remote-debugger 使用 27753 端口。
# 你可以从苹果开发者资源平台学习如何获取 UDID 。
> ios_webkit_debug_proxy -c 0e4b2f612b65e98c1d07d22ee08678130d345429:27753 -d
```

你也可以把 desired capability 中一个名为 `startIWDP` 的选项设置为 `true` (https://github.com/appium/appium/blob/master/docs/cn/writing-running-appium/caps.md) 。 Appium 会开启一个子进程运行上述命令并设置 udid ，所以你不再需要自己运行 ios_webkit_debug_proxy 。Appium 会监控 ios-webkit-debug-proxy，一旦崩溃就会重启。

``` 
// desired capabilities 示例
{
  "browserName": "Safari",
  "platformName": "iOS",
  "deviceName": "iPhone 7",
  "automationName": "XCUITest",
  "startIWDP": true,
  "udid": "auto"
}
```

你也可以使用 `ios-webkit-debug-proxy-launcher` —— Appium 代码库中的一个小脚本 —— 来启动代理。它会监控日志中的错误，并在需要时重启代理。
这是可选的而且有可能帮助到一些新的设备的使用：

``` 
# 修改 udid
# 注意，在 Appium 仓库中运行
> ./bin/ios-webkit-debug-proxy-launcher.js -c 0e4b2f612b65e98c1d07d22ee08678130d345429:27753 -d
```

**注意：** 为了允许建立连接，设备上需要打开 **"Web 检查器"**。在 **设置 >
safari > 高级**  中打开。

#### 指定非默认端口

Appium 期望 `ios-webkit-debug-proxy` 会在 `27753` 端口上运行。如果出于某种原因需要去改变默认的端口， `webkitDebugProxyPort` 能够通过设置代理的端口号来进行修改。

本文由 [CrazyForPoor](https://github.com/CrazyForPoor) 翻译。
