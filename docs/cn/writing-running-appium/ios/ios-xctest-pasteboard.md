## 基于WebDriverAgent/XCTest后台服务实现iOS自动化模拟器粘贴板操作

如果需要设置和读取iOS模拟器粘贴板内容 ，使用 Appium 是可行的。每个模拟器包含了各自的粘贴板。这个特性只从 Xcode SDK 8.1 开始支持。

在服务 WebDriverAgentRunner [直接运行在真机前台](https://github.com/appium/WebDriverAgent/issues/330)时，真机也可能支持此特性。

### mobile: setPasteboard

此命令将模拟器的粘贴板内容设置为作为参数传入的字符串。此外，也可以自定义给定字符串的编码。

#### 支持参数

 * _content_: 粘贴板的内容。之前的内容将被覆盖。此参数是必须有的。
 * _encoding_: 给定字符串的编码方式。默认是 UTF-8 。
 
 #### 用法示例
 
 ```java
 // Java
JavascriptExecutor js = (JavascriptExecutor) driver;
Map<String, Object> args = new HashMap<>();
args.put("content", new String(Files.readAllBytes(new File("/etc/passwd").toPath()), Charset.forName("latin-1")));
js.executeScript("mobile: setPasteboard", args);
  ```
  
  
### mobile: getPasteboard

此命令用于以字符串形式获取模拟器粘贴板当前的内容。此外，也可以自定义获取到的字符串的编码方式。

#### 支持参数

 * _encoding_: 收到的粘贴板内容的编码方式。默认是 UTF-8 。
 
 #### 用法示例
 
```python
# Python
content = driver.execute_script('mobile: getPasteboard', {'encoding': 'shift-jis'});
```



