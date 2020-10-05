## 如何在远程设备上执行Shell命令

可以在远程Android设备或被测模拟器上执行任何命令，并获取输出。此操作可能不安全，默认情况下在服务器端已禁用。在启动服务器时，必须提供命令行参数`--relaxed-security`才能启用远程Shell命令执行（以及其他默认禁用的不安全功能）。如果未在服务器端启用该命令行参数，并且尝试在客户端调用`mobile: shell`，则会引发异常。

### mobile: shell

在被测设备上执行给定的shell命令，并返回其`stdout`或同时返回`stdout`和`stderr`（如果`includeStderr`设置为`true`）。如果命令的返回码不为0，则将引发异常。该命令的执行动作与其在主机上通过`adb shell`执行的动作相同。

#### 支持的参数

- *command*：远程命令的名称。例如，它也可以是可执行文件的完整路径`/bin/ls`。该参数是强制性的。
- *args*：以字符串数组表示的命令参数列表。如果只提供单个字符串，则它将自动转换为单项数组。可选参数。
- *includeStderr*：将此参数设置为`true`，以便将`stderr`输出与`stdout`一起包括到返回的结果中。如果启用，则返回的结果将map包含相应的字符串键 `stdout`和`stder`，否则它只是一个简单的字符串。默认情况下为`false`。
- *timeout*：shell命令超时时间（以毫秒为单位）。如果该命令需要更多时间来完成执行，则将引发异常。默认为20000毫秒。

#### 用法示例

```java
// Java
Map<String, Object> args = new HashMap<>();
args.put("command", "echo");
args.put("args", Lists.newArrayList("arg1", "arg2"));
String output = driver.executeScript("mobile: shell", args);
assert output.equals("arg1 arg2");
```

```python
# Python
result = driver.execute_script('mobile: shell', {
    'command': 'echo',
    'args': ['arg1', 'arg2'],
    'includeStderr': True,
    'timeout': 5000
})
assert result['stdout'] == 'arg1 arg2'
```