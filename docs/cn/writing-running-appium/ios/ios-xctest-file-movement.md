## Pushing/Pulling 文件

Appium 提供了[Pull 目录](http://appium.io/docs/cn/commands/device/files/pull-folder/), [Pull 文件](http://appium.io/docs/cn/commands/device/files/pull-file/) 和 [Push 文件](http://appium.io/docs/cn/commands/device/files/push-file/) 三个命令来移动文件。

本文档旨在帮助理解它们是如何工作的。

### 命令使用格式

#### 名词解释：


bundle_id：bundle ID可以翻译成包ID,也可以叫APP ID 或应用ID,它是每一个ios应用的全球唯一标识。无论代码怎么改，图标和应用名称怎么换，只要bundle id没变，ios系统就认为这是同一个应用。每开发一个新应用，首先都需要到member center->identifier->APP IDS去创建一个bundle id。

container：每一个App都被放在沙盒（sandbox）中，在沙盒中，有一个Containers，Containers又被分为Bundle Container和Data Container

基本格式如下：

1. `@<app_bundle_id>:<optional_container_type>/<文件或者目录在container里的路径>`
2. `@<app_bundle_id>/<文件或者目录在container里的路径>`
3. `<文件或者目录在container里的路径>`

### 真机

#### 命令使用格式

以下是该方法参数的格式：

针对上面说的基本格式

- `@<app_bundle_id>` 是应用的 bundle identifier
- `optional_container_type` 是 container 类型
    - `documents` 是唯一选项
        - 你可以通过`ifuse -u <udid> --list-apps`得到 bundle id列表，然后给列表中的bundle id指定 container 类型为`documents`。
        - 比如下面的 _On My iPhone_ 图中有 _Slack_ 目录，但是在 `--list-apps` 中并不存在 `com.tinyspeck.chatlyio` 。所以我们就无法加载`com.tinyspeck.chatlyio@documents/`

            <img src='/docs/cn/writing-running-appium/ios/ios-xctest-file-movement/on_my_iphone.png' width=100>
    - 你也可以不指定container类型，比如 _格式 2_
        - 只有应用的`info.plist`里有 `UIFileSharingEnabled` 标签才可以加载。
- `文件或者目录在container里的路径` 指的是pull/push文件或者目录的目标。
    - 如果 `optional_container_type` 是 `documents`，那么这个路径可以映射为`Files`应用中的`On My iPhone/<app name>`

真机中不允许使用 _格式 3_

#### 示例

如果你想从 keynote 应用中把 _Presentation.key_ 拉到本地，你可以这样做：

- Pull file

```javascript
// webdriver.io
let data = driver.pullFile('@io.appium.example:documents/Presentation.key');
await fs.writeFile('presentation.key', Buffer.from(data, 'base64'), 'binary');
```

```ruby
# ruby_lib_core
file = @driver.pull_file '@com.apple.Keynote:documents/Presentation.key'
File.open('presentation.key', 'wb') { |f| f<< file }
```

该文件在  _Files_ 应用中的 _On My iPhone/Keynote_.

|Top | On  My iPhone | Keynote |
|:----:|:----:|:----:|
|![](/docs/cn/writing-running-appium/ios/ios-xctest-file-movement/top_files.png)|![](/docs/cn/writing-running-appium/ios/ios-xctest-file-movement/on_my_iphone.png)|![](/docs/cn/writing-running-appium/ios/ios-xctest-file-movement/keynote.png)|

如果文件目录比较深，比如 _On My iPhone/Keynote/Dir1/Dir2_，那么代码命令如下：

```javascript
// webdriver.io
let data = driver.pullFile('@io.appium.example:documents/Dir1/Dir2/Presentation.key');
await fs.writeFile('presentation.key', Buffer.from(data, 'base64'), 'binary');
```

```ruby
# ruby_lib_core
file = @driver.pull_file '@com.apple.Keynote:documents/Dir1/Dir2/Presentation.key'
File.open('presentation.key', 'wb') { |f| f<< file }
```

- Pull 目录

如果你要把 _On My iPhone/Keynote_ 拉到本地，你可以这样做： `@driver.pull_folder '@com.apple.Keynote:documents/'`。

```javascript
// webdriver.io
let data = driver.pullFolder('@io.appium.example:documents/');
await fs.writeFile('documents.zip', Buffer.from(data, 'base64'), 'binary');
```

```ruby
# ruby_lib_core
file = @driver.pull_folder '@com.apple.Keynote:documents/'
File.open('documents.zip', 'wb') { |f| f<< file }
```

- Push 文件

和 pull 文件一样

```javascript
// webdriver.io
driver.pushFile('@com.apple.Keynote:documents/text.txt', new Buffer("Hello World").toString('base64'));
```

```ruby
# ruby_lib_core
@driver.push_file '@com.apple.Keynote:documents/text.txt', (File.read 'path/to/file')
```

### 模拟器

#### 格式

参数格式如下：

针对上面说的基本格式

- `@<app_bundle_id>`
- `optional_container_type` 可选的容器类型
    - `app`, `data`, `groups` 或者 `<A specific App Group container>`
    - 如果不指定的话，默认使用 `app` container
- `文件或者目录在container里的路径`

_格式 3_ 只能处理 `app` container

#### 示例

```java
// Java
// Get AddressBook.sqlitedb in test app package ('app' container)
byte[] fileContent = driver.pullFile("Library/AddressBook/AddressBook.sqlitedb");
Path dstPath = Paths.get(new File("/local/path/AddressBook.sqlitedb"));
Files.write(dstPath, fileContent);
```

### 参考
- https://stackoverflow.com/questions/1108076/where-does-the-iphone-simulator-store-its-data
- https://stackoverflow.com/questions/48884248/how-can-i-add-files-to-the-ios-simulator
- https://apple.stackexchange.com/questions/299413/how-to-allow-the-files-app-to-save-to-on-my-iphone-or-to-on-my-ipad-in-ios/299565#299565
