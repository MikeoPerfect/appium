## 内存信息收集

从Node v. 12开始，可以收集Appium的内存使用信息来分析问题。 这对于分析内存泄漏问题非常有帮助。


### 创建dump文件

为了在任意时间创建dump文件，执行`node`进程时增加如下命令行参数，这会执行appium.js脚本：

```
--heapsnapshot-signal=&lt;signal&gt;
```

这里的 `signal` 可以是一个有效的自定义信号，例如 `SIGUSR2`。然后你就可以

```
kill -SIGUSR2 &lt;nodePID&gt;
```

dump文件会被存放在Appium主脚本执行路径下。文件扩展名为 `.heapsnapshot`，文件可以在Chrome Inspector中加载来进行分析。 

### dump文件分析

详细信息请查看[Rising Stack article](https://blog.risingstack.com/finding-a-memory-leak-in-node-js/)。
