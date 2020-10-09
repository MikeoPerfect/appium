## 自动化性能度量

Apple 提供了一套工具`instruments`，这套工具有着非常多的功能，可以用来测量桌面端和手机端应用的性能。收集到的数据可以用 `Instruments.app`显示出来，这是 Xcode DevTools 的一部分。Xcode 默认提供了几个度量模板，比如 `Activity Monitor` 或 `Time Profiler`，同时我们也可以创建自己的配置文件，并自定义选择一组衡量标准来记录或可视化。读 https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide 去获取更多可用工具的详细功能概述。

### mobile: startPerfRecord

此命令启动被测设备上给定的配置文件名称(模板)的性能记录器。如果这个命令在一行被调用两次或更多次，上一次的记录器将被强制停止，新的记录器将会启动。所有的之前的数据都会丢失。

### 支持参数

 * _timeout_: 表示记录器应该运行多长时间(以毫秒为单位)。默认是5分钟。尽量不要设置太高的值，因为 `instruments` 工具生成的 .trace 文件相当大。
 * _profileName_: 现有性能模板的名称。 默认是 `Activity Monitor`。
 * _pid_: 测量性能进程的ID。将其设置成 `current` ，以便我们只衡量进程的性能，该进程属于当前活动的应用程序(这可能对一些配置文件不起作用)。 如果进程ID未设置(默认设置)，将测量设备上运行的所有进程的性能。当待测设备是模拟器时， 设置进程ID可能需要使用sudo特权启动`instruments`工具，这是不受支持的，并且会抛出超时异常。
 
 #### 用法示例

```java
// Java
Map<String, Object> args = new HashMap<>();
args.put("timeout", 60 * 1000);
args.put("profileName", "Time Profiler");
driver.executeScript("mobile: startPerfRecord", args); 
```
    
### mobile: stopPerfRecord
    
此命令停止被测设备上给定配置名称(模板)的性能记录器，并以压缩格式返回收集到的数据或上传到远程服务器上。如果`startPerfRecord`命令未被调用则会抛出异常。

重要提示：为了度量模拟器性能，需要在 Appium 服务器命令行设置合适的[安全标记](/docs/cn/writing-running-appium/security.md)，因为`instruments`工具会记录在主机上运行的所有进程。

#### 支持参数
 * _profileName_: 之前已经运行监视的现有性能模板的名称。默认是`Activity Monitor`。
 * _remotePath_: 远程位置的路径，会将压缩后的.trace文件上传至该路径。支持以下协议：http/https, ftp。Null 或者空字符串(默认配置)表示结果文件内容应该被压缩，以Base64编码并作为返回值传递。如果生成的文件太大，无法装入可用的服务器进程存储，会抛出异常。
 * _user_: 用于远程身份验证的用户名。只有在提供 `remotePath`参数时才有效。
 * _pass_: 远程身份验证的密码。只有在提供 `remotePath`参数时才有效。
 * _method_: http分片上传方法名。只有在提供 `remotePath`参数时才有效。
 
 #### 用法示例
 
```python
# Python
driver.execute_script('mobile: stopPerfRecord', {
    'profileName': 'Time Profiler',
    'remotePath': 'ftp://myserver/upload/',
    'user': 'serveruser',
    'pass': 'secretpass'
})
```
