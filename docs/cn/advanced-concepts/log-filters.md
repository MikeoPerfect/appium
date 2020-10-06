## Appium日志过滤

有时我们需要在系统日志中隐藏一些敏感信息，比如密码，标识符，哈希等。从Appium 1.18.0版本开始支持使用 `--log-filters` 命令行参数。通过这个参数，我们可以设置日志模糊处理规则文件的路径，文件可包含一个或多个规则。


### 配置格式

过滤配置必须是包含过滤规则数组的有效JSON文件。每条规则都是具有一组预定义属性的对象。支持的规则属性如下：

- `pattern`: 要替换的有效Javascript正则表达式模式。必须是有效的非空模式。
- `text`: 要替换的简单的非空提取文本。`text`属性或者`pattern` 属性必须至少提供一个。如果两者都提供了， `pattern`优先级更高。 
- `flags`: 给定pattern 的正则表达式标志。支持的标志与标准的JavaScript正则表达式相同： https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Advanced_searching_with_flags_2。 'g' (全局搜索)标志一直是启用的。
- `replacer`: 要使用的替换值。默认为 `**SECURE**`。也可以是空值。


### 配置示例

日志中，使用默认值 `**SECURE**` 替换所有的`my.magic.app`:

```json
[
    {
        "text": "my.magic.app"
    }
]
```

日志中，使用自定义的值（***）替换所有的`my.magic.<any char>` 字符串（不区分大小写）：

```json
[
    {
        "pattern": "my\\.magic\\.\\w",
        "flags": "i",
        "replacer": "***"
    }
]
```

日志中，使用自定义的值（***）替换所有的 `my.magic.<any chars>` 和/或者 `your.magic`  字符串（不区分大小写）：

```json
[
    {
        "pattern": "my\\.magic\\.\\w+",
        "flags": "i",
        "replacer": "***"
    },
    {
        "pattern": "your\\.magic",
        "flags": "i",
        "replacer": "***"
    }
]
```

截断所有日志，每行最多15个字符（高级用法）：

```json
[
	{
        "pattern": "(.{1,15}).*",
        "flags": "s",
        "replacer": "$1"
    }
]
```


### 配置错误处理
如果任何配置规则中包含无效项（比如空/无效的pattern，空规则等）。Appium会打印收集到的错误信息的详细报告，并且在问题被解决之前将无法启动。
