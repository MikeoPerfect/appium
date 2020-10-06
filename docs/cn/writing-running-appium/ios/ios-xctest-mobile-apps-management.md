## 基于WebDriverAgent/XCTest的iOS应用管理命令进阶版

从XCode9开始，我们可以在同一个session里管理多个应用。那我们就可以在被测应用压后台之后，打开iOS设置，去改变一些设置，然后恢复被测应用或者检查对应场景，事实上，改变设置，会使应用退出或者重启。针对iOS系统，Appium有一组特殊的子命令`mobile:`可以提供这些功能的交互。

**重要提示：** 确保在应用重启之间，你没有缓存 WebElement 实例，因为每次重启之后，它们都会变成无效实例。

### mobile: installApp

将应用安装到被测机器上。如果设备上安装过该应用，应用会被覆盖安装，这样可以允许你测试应用升级。在安装被测应用的时候，要注意：确保`terminateApp`先调用，否则WebDriverAgent会认为这是应用闪退。

#### 支持的参数

 * `app`: 应用的路径， .ipa/.app 文件在服务端文件系统里的路径，
   或者 .app 的zip压缩包，或者 URL 指向网上的 .ipa/.zip 的文件的URL。必填参数。

#### 使用案例

```java
// Java
Map<String, Object> params = new HashMap<>();
params.put("app", "http://example.com/myapp.ipa");
js.executeScript("mobile: installApp", params);
```


### mobile: removeApp

卸载被测设备上的应用。这个接口不会验证被卸载的应用是否已经安装过。

#### 支持的参数

 * `bundleId`: 必填参数，被卸载应用的bundleId

#### 使用案例

```python
# Python
driver.execute_script('mobile: removeApp', {'bundleId': 'com.myapp'});
```


### mobile: isAppInstalled

验证应用是否在设备上安装，返回`true` 或者 `false`。

#### 支持参数


 * `bundleId`: 必填参数，应用的bundleId

#### 使用案例

```java
// Java
Map<String, Object> params = new HashMap<>();
params.put("bundleId", "com.myapp");
final boolean isInstalled = (Boolean)js.executeScript("mobile: isAppInstalled", params);
```


### mobile: launchApp

启动设备上的应用，如果应用已经启动，会加载到前台。

#### 支持参数

 * `bundleId`: 必填参数，应用的bundleId
 * `arguments`: 可选参数，命令行参数列表。
 * `environment`: 可选参数，环境变量的key/value值

#### 使用案例

```python
# Python
driver.execute_script('mobile: launchApp', {'bundleId': 'com.myapp',
                                            'arguments': ('-foo', '--bar'),
                                            'environment': {'foo': 'bar'}})
```


### mobile: terminateApp

终止设备上的应用。如果应用没有在运行，返回`false`，否则`true`

#### Supported arguments

 * `bundleId`: 必填参数，应用的bundleId

#### 使用案例

```java
// Java
Map<String, Object> params = new HashMap<>();
params.put("bundleId", "com.myapp");
final boolean wasRunningBefore = (Boolean)js.executeScript("mobile: terminateApp", params);
```


### mobile: activateApp

激活被测设备上的应用，并加载到前台。应用必须已经在运行。如果应用已经在前台，该调用会被忽略。

#### 支持参数

 * `bundleId`: 必填参数，应用的bundleId

#### 使用案例

```python
# Python
driver.execute_script('mobile: activateApp', {'bundleId': 'com.myapp'});
```


### mobile: queryAppState

查询设备上应用的当前状态。有五种可能的状态（详见[Apple's documentation](https://developer.apple.com/documentation/xctest/xcuiapplicationstate?language=objc)）：

 * `0`: unknown，当前状态未知
 * `1`: 没有在运行
 * `2`: 后台挂起
 * `3`: 后台未挂起
 * `4`: 前台运行

#### 支持参数

 * `bundleId`: 必填参数，应用的bundleId

#### 使用案例

```java
// Java
Map<String, Object> params = new HashMap<>();
params.put("bundleId", "com.myapp");
final int state = (Integer)js.executeScript("mobile: queryAppState", params);
```
