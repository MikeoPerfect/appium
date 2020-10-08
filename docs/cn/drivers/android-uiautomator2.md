
## Android的UiAutomator2驱动

Appium对Android应用程序自动化的最大支持是通过`UiAutomator2`driver实现的。_(是Appium的新手? 请阅读 [Appium drivers介绍](#TODO))_。这个驱动程序是利用Google的 [UiAutomator2](https://developer.android.com/training/testing/ui-automator.html) 技术来促进实现设备或模拟器上的自动化。

在[appium-uiautomator2-driver](https://github.com/appium/appium-uiautomator2-driver) 收购了UiAutomator2 driver后，它开始发展。

旧版的Android drivers包括：

* [UiAutomator的驱动](/docs/en/drivers/android-uiautomator.md)

### 要求和支持

除了Appium的一般要求外，还需要具备以下条件:

* Java 8需要被正确安装和配置在你的平台上
* 具备能运行Android SDK的Mac, Windows, 或者Linux OS 

此外，UiAutomator2 driver不支持低于5.0的Android版本（Lollipop，API级别21）。如果要自动执行这一类的版本，请考虑使用 [UiAutomator驱动](/docs/en/drivers/android-uiautomator.md)。

### 使用

使用UiAutomator driver启动会话的方法是在[新的会话请求](#TODO)的[capability](#TODO)参数设置中包括属性 `automationName` ，对应的值为`UiAutomator2`。当然了，capabilities的参数设置中中还必须至少包含有正确的`platformName`（= `Android`）`platformVersion`，`deviceName`和`app` 这些参数信息。

强烈建议还设置`appPackage`和`appActivity` 功能，以使Appium确切知道应为应用程序启动哪个程序包和活动。否则，Appium会尝试从应用清单中自动确定这些内容。

### Capabilities

UiAutomator2 driver支持许多标准的 [Appium capabilities](/docs/en/writing-running-appium/caps.md)，但也有一组额外的功能，这些功能可调节driver的行为。这些可以在前面提到的文档的[Android部分](https://github.com/testerhome/appium/blob/master/docs/en/writing-running-appium/caps.md#android-only)中找到。

对于web端的测试，要去自动化驱动Chrome而不是应用程序，则需要将`app` 功能参数保留为空，并且将`browserName`功能参数设置为 `Chrome`。请注意，您有责任确保Chrome是在模拟器/设备上，并且它的版本与Chromedriver兼容。


### Commands指令

需要查看Appium支持的各种命令，特别是关于命令如何映射到UiAutomator2 driver行为的信息，请参阅[API参考](https://github.com/testerhome/appium/blob/master/docs/en/drivers/android-uiautomator2.md#TODO)。


### 基本设置

1. 确保您已安装和配置了Appium的常规依赖项（例如Node＆NPM）。
  
1. 确保已安装Java（JDK，而不仅仅是JRE），并且Java二进制文件已添加到您的路径中。对于Mac / Linux和Windows，此步骤的说明有所不同。请查阅特定于平台的文档，因为这是一项常见的任务。如何更改Windows的路径的一个例子是 [在这里](https://www.java.com/en/download/help/path.xml)。
  
1.  确保`JAVA_HOME`环境变量也设置为JDK路径。例如，对于Mac / Linux（此路径的具体情况因系统而异），请将其放入您的登录脚本中：
  
    ```
 export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home"
    ```
   
   在Windows上，这可以通过使用与设置上面的PATH相同的策略在控制面板中设置环境变量来完成。 [Android Studio](https://developer.android.com/studio/index.html)也包含有JDK路径，比如`/Applications/Android Studio.app/Contents/jre/jdk/Contents/Home`（Mac）。您也可以指定路径。

1. 安装[Android SDK](http://developer.android.com/sdk/index.html)。现在支持此操作的方法是使用[Android Studio](https://developer.android.com/studio/index.html)。使用提供的GUI将Android SDK安装到您选择的路径。
  
1. 设置`ANDROID_HOME`环境变量以匹配此路径。例如，如果您将SDK安装到`/usr/local/adt`，则通常在`sdk`其中包含SDK文件的文件夹中。在这种情况下，在Mac和Linux，下面一行添加到您的登录脚本（例如， `~/.bashrc`，`~/.bash_profile`等...）：
  

   在Windows上，按照与之前相同的步骤在控制面板中设置环境变量。
   
1. 使用SDK管理器，确保已安装要自动化的Android API级别的SDK（例如24）。
  
1. 在Windows上，请确保始终在管理员模式下运行Appium。

至此，您的基本系统设置完成。根据您要自动化仿真器还是真实设备来执行以下步骤。另外，在运行测试时，您将需要应用程序的APK（最好是在Debug模式下构建）的路径或URL作为capability属性中`app`参数的值。

### 模拟器设置

为了在模拟器上运行测试，请使用包含了Android Studio或SDK的AVD Manager。使用此工具，创建符合您需求的模拟器。启动模拟器后，Appium将自动找到并用于测试。否则，如果您使用`avd`与模拟器名称匹配的值指定功能，则Appium将尝试为您启动模拟器。

模拟器的其他提示：

* 尽管有其自身的局限性，但存在适用于Android的硬件加速模拟器。这个可以从英特尔网站或通过Android SDK Manager安装。有关更多信息，请转到 [此处](https://github.com/intel/haxm)。
* 如果要运行任何Appium测试，或使用任何电源命令，请确保`hw.battery=yes`在AVD `config.ini`中进行设置。（从Android 5.0开始，这是默认设置。）

### 真实设备设置

对于Android自动化，除了以下简单要求之外，不需要其他设置即可在真实设备上进行测试：

* 确保为设备打开了[开发者模式](https://developer.android.com/studio/debug/dev-options.html)。
* 确保设备通过USB连接到Appium主机，并且可以被[ADB](https://developer.android.com/studio/command-line/adb.html)找到 （运行`adb devices`以确保）。
* 确保禁用设置中的“验证应用程序”，以允许Appium的助手应用程序运行而无需手动干预。

（对于某些特定命令，设备可能需要root，尽管这不是必须的。）

