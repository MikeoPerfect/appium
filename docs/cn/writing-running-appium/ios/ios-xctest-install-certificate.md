## 在 iOS 上自动安装自签名的证书

不幸地是，苹果未提供任何命令行选项，可以帮助在真机或者模拟器上安装自签名的证书。然而，有一个[over-the-air](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/iPhoneOTAConfiguration/Introduction/Introduction.html) 技术允许安装部署几种实体类型，包括这种自签名的证书，只需要简单地通过内置的浏览器下载准备的证书文件即可。文件下载好之后，就根据简单向导步骤就可以安装，信任自签名证书了。


### mobile: installCertificate

 After the certificate is installed the script is going to open System Preferences again and enable it inside Certificate Trust Settings if it is disabled.
该命令接收PEM格式的证书内容，将证书内容转成一种特殊格式，然后部署到Appium内置的HTTP服务器上。这样被测试的设备就可以下载到证书了。因此我们需要被测试的设备可以通过Appium Server运行的机器的hostname和端口访问Appium Server。如果证书信任设置未激活，在证书安装好之后，脚本会打开System Preference，让你去激活证书。

#### 支持的参数

 * _content_: 证书内容是一串 base64 编码的字符串。该参数是必填的。

#### 使用用例

```java
// Java
Map<String, Object> args = new HashMap<>();
byte[] byteContent = Files.readAllBytes(new File("custom.cer").toPath());
args.put("content", Base64.getEncoder().encodeToString(byteContent));
driver.executeScript("mobile: installCertificate", args);
```
