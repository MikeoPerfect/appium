## 从源码运行Appium

你想从源码运行Appium并帮助修复BUG和添加功能吗？
真棒！只需要fork工程，添加一个修改，然后发送pull请求即可！
在开始之前请阅读我们的代码风格指南（[Style Guide](style-guide.md)。
在发送pull请求前请确保通过单元和功能测试；关于如何运行测试等更多信息，请继续阅读！

### Node.js

Appium 使用 JavaScript 编写，运行在 [Node.js](https://nodejs.org/) 引擎里，目前支持 Node.js 6及以上版本。强烈推荐使用版本管理器，以便 Node.js 可以全局安装在系统上。
* NVM - [https://github.com/creationix/nvm](https://github.com/creationix/nvm)
* N - [https://github.com/tj/n](https://github.com/tj/n)

为了方便Appium管理依赖，安装 Node.js 同时，也需要安装 [NPM](https://www.npmjs.com/) 包管理工具。Appium 支持 NPM 3及以上版本。

（翻译备注：新版的 Node.js 已经集成了NPM，所以在安装 Node.js 时候，NPM 也一起安装好了）


### 从源码配置 Appium

Appium 的配置涉及：

1. Appium Server —— 在你的测试代码和设备或模拟器之间通过 Appium Server 来回发送消息
2. 测试脚本 —— 任何客户端语言都可以，只要和 Appium 兼容

运行 Appium Server，然后运行你的测试。

快速开始：

```center
git clone https://github.com/appium/appium.git
cd appium
npm install
npm run build
node .
```


### 捣鼓改造 Appium

安装 [appium-doctor](https://github.com/appium/appium-doctor)，运行 appium-doctor，验证所有依赖是否都正确安装完成（因为构建 Appium 的依赖，和运行是 Appium 的依赖是不同的）：

```
npm install -g appium-doctor
appium-doctor --dev
```
安装 Node.js 依赖:
```
npm install
```

当从 GitHub 中拉新代码时，如果`package.json`有更改，需要删除旧的依赖关系并重新运行`npm install`：

```
rm -rf node_modules && rm -rf package-lock.json && npm install
```

此时，您将可以启动 Appium Server：

```center
node .
```

完整的参数列表，请参考[the server documentation](/docs/cn/writing-running-appium/server-args.md)

#### 鼓捣 iOS 上的Appium

为了避免启动iOS应用程序时可能出现的安全对话框，您必须通过以下两种方式之一修改`/etc/authorization`文件：

1. 手动修改`/etc/authorization`文件中的`<key>system.privilege.taskport</key>`下的`<allow-root>`的值为`<true/>`。
2. 运行以下命令，为您自动修改`/etc/authorization`文件：

   ```center
    sudo npm run authorize-ios
	```

此时，运行：

```
rm -rf node_modules && rm -rf package-lock.json && npm install
```

现在你的 Appium 实例已经准备好了。运行`node .`以启动Appium服务器。

#### 鼓捣 Android 上的Appium

确保已安装`ant`、`maven`、`adb`且已添加到 PATH 环境变量，还需要安装 android-19及以上版本的 sdk。在 Appium 本地仓库打开命令行，使用以下命令安装/运行以下包：

通过运行以下命令配置 Appium：

```
rm -rf node_modules && rm -rf package-lock.json && npm install
```

确保您只有一个 Android 模拟器或设备运行，例如，通过在另一个进程中运行此命令（假设`emulator`命令在您的路径上）：

```center
emulator -avd <MyAvdName>
```

现在，您可以通过`node .`运行Appium服务器了。

#### 确保你的代码是最新的

由于Appium使用某些软件包的开发版本，因此通常需要安装新`npm`软件包或更新各种软件。运行`npm install`将更新所需的一切。当 Appium 升级版本时，您还需要执行此操作。在运行`npm install`之前，建议先删除`node_modules`目录中的所有旧依赖项：

```
rm -rf node_modules && rm -rf package-lock.json && npm install
```

### Different packages

Appium 由大量不同的包组成，虽然可以在单个包中运行，但通常情况下，无论是修复bug还是添加新功能，都需要同时运行在在多个包之上。

运行`npm install`安装的都是已发布的依赖，而有些情况下，我们需要连接本地开发版本的包。

当包`A`依赖包`B`，以下步骤可以连接这两个包：

1. 打开一个终端，进入包`B`
   ```
    cd B
   ```
2. 使用 [NPM link](https://docs.npmjs.com/cli/link) 为包`B`，创建符号链接（symbolic link）
   ```
    npm link
   ```
3. 打开另一个终端，进入包`A`
   ```
    cd A
   ```
4. 使用 [NPM link](https://docs.npmjs.com/cli/link) 连接依赖包`B`的开发版本
   ```
    npm link B
   ```

这样`A`使用的`B`的版本，就是你本地的开发版本了。
但是这样的 JavaScript 更改，只在被转换（transpiled）时生效。
如果你准备从包`A`开始测试，需要在包`B`目录下运行`npm run build`.


### 运行测试

首先，请查看我们关于[running tests in
general](/docs/cn/writing-running-appium/running-tests.md) 的文档，确保您的系统正确设置为您希望测试的平台。

一旦您的系统配置完毕，您的代码是最新的，您可以运行单元测试：

```center
npm run test
```

您可以用以下命令，对所有受支持的平台运行功能测试（确保在另一个窗口中运行Appium`node .`）：

```center
npm run e2e-test
```

### 调试 Node

本项目在[VSCode](https://code.visualstudio.com/)中运行 NodeJS 代码，有多个启动配置项：

* _Debug_: debug 模式运行 Appium 服务，这样就能在 VSCode 源文件里设置断点了
* _Attach Debug_:连接到当前运行中的 Appium 服务
  * 用法示例
    * 根路径运行`node --inspect-brk . --port 5555`
    * 运行`attach debug`
    * 在 VSCode 里设置断点
* _Test All_:运行`test/`路径下的所有 mocha tests, 测试代码、源码里都可以设置断点
* _Test Current File_:只运行当前的选中的 mocha 文件。如果不是有效的mocha test，就会运行失败。

（翻译说明：Mocha 是一个 JS 测试框架）

### 提交代码

每个 Appium 包都会配置一个检查（pre-commit）hook，在提交完成前，这个 hook 会运行 [linter](https://eslint.org/) 和单元测试，这个过程中出现任何错误，都会阻止本次提交。

只要往 [GitHub](https://github.com/)上的 Appium 仓库，提交代码以及创建 [pull request](https://help.github.com/articles/about-pull-requests/)，Appium 构建系统就会执行所有功能测试。

本文由 [校长](https://testerhome.com/xushizhao) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。