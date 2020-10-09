## 在安装多个 Xcode 版本的情况下运行Appium

如果你的电脑上安装了多个 Xcode，你可能需要从以下2种方法里选一个工具集供 Appium 使用:

### xcode-select tool

仅 sudo 权限可用，会影响整个系统。

假如你选择了 `/Applications/Xcode7.app`:

1. 设置默认 Xcode
  ```
  sudo xcode-select -s /Applications/Xcode7.app/Contents/Developer
  ```
2. 运行 Appium (使用命令行 或者 使用GUI)
  ```
  appium
  ```

### 环境变量

不需要权限，只影响当前 shell，因此 Appium 必须使用此 shell 启动

假如你选择了 `/Applications/Xcode9.app`:
1. 设置`DEVELOPER_DIR`环境变量
  ```
  export DEVELOPER_DIR=/Applications/Xcode9.app/Contents/Developer
  ```
2. *从相同的shell*里运行 Appium
  ```
  appium
  ```

本文由 [nicole1010](https://github.com/nicole1010) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。