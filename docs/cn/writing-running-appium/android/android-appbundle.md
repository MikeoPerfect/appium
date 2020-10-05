- ## 如何测试Android App Bundle

  Google已发布了[Android App Bundle](https://developer.android.com/platform/technology/app-bundle/)功能。

  该功能会生成一个`.aab`文件，我们应该将其上传到Google Play商店。我们可以使用官方管理工具[bundletool](https://developer.android.com/studio/command-line/bundletool)（它可从[bundletool](https://github.com/google/bundletool)下载）通过CLI管理`.aab`文件。[该指南](https://developer.android.com/guide/app-bundle/)可以帮助我们了解此功能。

  我们可以通过CLI从`.aab`文件中获取apk文件。我们可以使用生成的文件针对发布模块进行测试。从Appium 1.9.2开始，您可以使用UiAutomator2驱动程序对文件`.apks`进行Appium测试。链接[1](https://github.com/appium/appium-adb/pull/367)和[2](https://github.com/appium/appium-base-driver/pull/271)是该功能的PR。

  ## 如何进行测试

  1. 导出`bundletool.jar`到你的路径中

     - Appium会在本地环境路径中寻找`bundletool.jar`。确保其可以找到带有`'bundletool.jar'`的路径。如果找不到，请设置正确的路径。

  2. 从 `.aab`文件生成`.apks`文件

     - `.aab`在Android Studio超过3.2的版本中可用

     - 从`.aab`生成`.apks`文件时时，必须正确签名。此步骤需要数据签名。

       ```bash
       $ java -jar apks / bundletool.jar build-apks \
         --bundle apks / release / release / app.aab \ # 生成的aab文件
         --output apks / AppBundleSample.apks \        # 您要输出的apks文件
         --ks apks / sign \                            # 签名密钥库
         --ks-key-alias KEY0 \                         # 密钥库别名
         --ks-pass pass：kazucocoa \              	   # 密钥库的密码
         --overwrite                                   # 覆盖任何现有的apk文件
       ```

  3. 使用`.apks`文件的路径作为您的app capability。

     ```ruby
     required_capability  =  caps:{ 
         platformName: :android,
         automationName: 'uiautomator2',
         platformVersion: '8.1',
         deviceName: 'Android Emulator',
         app: 'path/to/your.apks',   #这行很重要
         fullReset: true,
         ...
     }
     
     core = ::Appium::Core.for(desired_capability)
     driver = core.start_driver
     ```

  您可以在[https://developer.android.com/guide/app-bundle/](https://developer.android.com/guide/app-bundle/)中找到获取测试APK的另一种方法。

  

  ## 提示

  ### 使`bundletool.jar`可执行

  确保bundletool是可执行的，例如使用以下命令。

  `$ chmod 655 /path/to/bundletool.jar`

  

  ### 用不同的语言测试

  如果要使用其他语言资源对应用程序进行测试，设置`fullReset: true`。

  Appium仅按照appbundle功能的行为安装最少的资源集。例如，如果设备的语言设置为英语，则Appium将仅安装`en`资源。安装的apk将没有日语资源。

  为了强制使用其他语言资源集重新安装，请指定参数 `fullreset: true`

  ## 示例项目

  - https://github.com/KazuCocoa/AppBundleSample
