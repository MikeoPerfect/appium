## 使用Appium的Android设备屏幕流

Appium从1.16开始，可以将被测设备的屏幕流式传输到一个或多个远程客户端。当前显示的内容通过http协议作为可配置的[MJPEG](https://en.wikipedia.org/wiki/Motion_JPEG)流广播。这样可以观察自动化测试在运行时的执行情况，并尽早发现可能的问题。单个MJPEG服务器支持多个并发客户端，这些客户端可以同时接收屏幕更新。那里的帧速率取决于服务器和设备的性能，但是接近实时速率，可以达到每秒60帧，尤其是在适当调整比特率和/或缩放屏幕尺寸的情况下。

### mobile: startScreenStreaming

开始流式传输设备的屏幕。仅在满足所有要求的情况下才能开始流传输：

- [GStreamer](https://gstreamer.freedesktop.org/)二进制文件已安装在服务器计算机上。例如，可以使用以下命令在Mac OS上安装它：`brew install gstreamer gst-plugins-base gst-plugins-good gst-plugins-bad gst-plugins-ugly gst-libav`
- 被测设备有`screenrecord`程序，并且该程序支持`--output-format=h264`参数选项。模拟器仅从API 27开始有此程序。
- `adb_screen_streaming` [服务器功能](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/security.md)被启用。

该命令使用adb初始化低级流，将其通过管道传输到GStreamer管道，该管道将h264编码的帧转换为JPEG图像并将其发送到TCP套接字。在此序列的末尾有Node.js http服务，该服务将TCP流包装为HTTP协议，因此可以使用常规浏览器观看视频。如果流媒体已在运行，则命令仅静默返回。不支持同时在多个端口/不同的配置的设备进行流传输。在开始新的流之前，必须先停止当前流。

#### 支持的参数

- *width*：生成的图像所需的宽度。如果该参数未设置，则默认设置为设备屏幕的实际宽度。如果该`width`值小于原始值，则将缩放输出流。建议在设置自定义宽度/高度时保留原始比例。
- *height*：生成的图像所需的高度。如果该参数未设置，则默认设置为设备屏幕的实际高度。如果该`height`值小于原始值，则将缩放输出流。建议在设置自定义宽度/高度时保留原始比例。
- *bitRate*：原始的h264编码的视频流的比特率。默认情况下，它等于4000000 bit / s。如果在生成的MJPEG视频中发现严重的帧丢失，建议将其设置为较低的值。
- *host*：用于启动HTTP MJPEG服务的IP地址/主机名。您可以将其设置为`0.0.0.0`,触发所有可用网络接口上的广播。默认情况下为`127.0.0.1`。
- *port*：用于启动HTTP MJPEG服务器的端口号。默认情况下为`8093`。
- *pathname*：MJPEG服务可用的HTTP请求路径。如果该参数未设置，则给定`host`/`port`组合上的任何路径名都可以使用。请注意，该值应始终以单个斜杠开头：`/`
- *tcpPort*：用于启动内部TCP MJPEG广播的端口号。此类广播始终在环回接口（`127.0.0.1`）上开始。默认情况下为`8094`。
- *quality*：流式JPEG图像的质量值。此数字应在[1，100]范围内，其中100是最佳质量。默认情况下为`70`。
- *thinkRotation*：如果设置为，`true`则GStreamer管道将增加生成的图像的尺寸，以使图像横向和纵向都正确适合。`true`如果在广播会话期间设备旋转不会相同，请将其设置为。`false`默认情况下。
- *logPipelineDetails*：是否将GStreamer管道事件记录到标准日志输出中。用于调试作用较大。默认情况下为`false`。

#### 用法示例

```java
// Java
Map<String, Object> args = new HashMap<>();
args.put("width", 1080);
args.put("height", 1920);
args.put("considerRotation", true);
args.put("quality", 45);
args.put("bitRate", 500000);
driver.executeScript("mobile: startScreenStreaming", args);
```

```python
# Python
driver.execute_script('mobile: shell', {
    'width': 1080,
    'height': 1920,
    'considerRotation': True,
    'quality': 45,
    'bitRate': 500000,
})
```

### mobile: stopScreenStreaming

停止正在运行的屏幕流session。如果之前没开始任何session，则不执行任何操作。请注意，一旦终止容器driver的session，屏幕流session会自动停止。

#### 用法示例

```java
// Java
driver.executeScript("mobile: stopScreenStreaming");
```

```python
# Python
driver.execute_script('mobile: stopScreenStreaming')
```
