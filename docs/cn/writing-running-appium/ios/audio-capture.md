## 从 iOS 模拟器和真机中捕获语音


### 客户端侧 API

从 Appium 1.18.0 开始，就可以在 iOS 上录制语音并在客户端侧将语音保存到文件中去。苹果并未提供
任何可以直接从模拟器或者真机中获取语音流的接口。但是我们可以将语音流重定向到宿主机器上，这样就可以捕获语音流了。

#### mobile: startAudioRecording

根据给定的语音压缩参数，开始在指定的主机上录制语音。

#### 支持的参数

 * _audioInput_: 用来捕获语音的输入设备名字，比如 `:1`。在终端使用 `ffmpeg -f avfoundation -list_devices true -i ""`命令可以列出所有的捕获设备。该参数为必填参数。
 * _audioCodec_: 语音解码器的名字. 默认是`aac`。
 * _audioBitrate_: 语音流的码率，默认是`128k`。
 * _audioChannels_: 生成的语音流的声道数量。设置为 `1` 就会创建单声道的语音流。默认是 `2`。
 * _audioRate_: 采样率。默认 `44100`。
 * _timeLimit_: 最长录音时间，单位秒。默认是 `180`，最长为 `43200` (12 hours)。
 * _forceRestart_: 当调用 startRecordingAudio 时，是否要强制重启语音录制过程，或者忽略该调用，直到当前语音录制完成。默认是 `false`，即不强制重启。

#### mobile: stopAudioRecording

停止语音录制流程（之前通过调用startAudioRecording启动）。stopAudioRecording 方法的返回结果是一个base64位编码的 .mp4 文件，该文件录制了从 `startAudioRecording` 调用开始的语音。如果之前`startAudioRecording`没有调用过，会产生一个空字符串。

#### 示例

```java
// Java
driver.executeScript("mobile: startAudioRecording", ImmutableMap.of("audioInput", ":1"));
Thread.sleep(10000);
byte[] mp4Data = Base64.getMimeDecoder()
  .decode((String) driver.executeScript("mobile: stopAudioRecording"));
try (FileOutputStream fos = new FileOutputStream("out.mp4")) {
   fos.write(mp4Data);
}
```

```ruby
# Ruby
@driver.execute_script 'mobile: startAudioRecording', audioInput: ':0'
sleep 10
base64_str = @driver.execute_script 'mobile: stopAudioRecording'
File.write 'out.mp4', Base64.decode64(base64_str)
```

```python
# Python
driver.execute_script('mobile: startAudioRecording', {'audioInput': ':1'})
time.sleep(10)
base64_str = driver.execute_script('mobile: stopAudioRecording')
with open('out.mp4', 'wb') as f:
    f.write(base64.b64decode(base64_str))
```

### 服务端所需配置

Appium 的版本需要大于等于 1.18.0。

宿主机必须安装了 [FFMPEG](https://www.ffmpeg.org/download.html)，并且该命令已经配置到系统路径中去了。在 macOS 上，可以通过 [Brew](https://brew.sh/) 命令安装：`brew install ffmpeg`。

macOS 从 10.15 开始，macOS需要可以录制语音的应用必须显示激活。激活路径：System Preferences->Security & Privacy->Privacy->Microphone tab。
确保 FFMPEG 或者 Appium 进程 (比如 Terminal) 在激活列表中。

该功能有潜在的安全风险，所以必须在服务端侧显示允许。该功能的名字是 `audio_record`。更多细节参见[Security](/writing-running-appium/security.md) 。


### 模拟器设置

在 iOS 模拟器上进行语音录制，需要进行如下配置：

* 安装 [Soundflower](https://github.com/mattingalls/Soundflower/releases)
* 将模拟器的语音输出重定向到 Soundflower。 在 模拟器的主菜单选择 I/O->Audio Output->Soundflower (2ch)。
* 在终端运行 `ffmpeg -f avfoundation -list_devices true -i ""` 得到 `Soundflower (2ch)` 的标识名字。这个标识使用 `:` 做为前缀。把这个标识作为 `audioInput` 的参数来调用 `mobile: startAudioRecording`。
* 测试你的配置是否生效。在模拟器里播放任意一个录音，然后在终端执行该命令：`ffmpeg -t 5 -f avfoundation -i ":1" -c:a aac -b:a 128k -ac 2 -ar 44100 -y ~/Desktop/out.mp4`（注意-i的参数值需要设置为上一步得到的值）。5秒后，在你的桌面就会有一个 `out.mp4` 文件，该文件录制了刚刚的语音。


### 真机设置

在真机上进行语音录制，需要进行如下配置：

* 将你的真机设备和mac电脑链接。
* 运行 `open -a /System/Applications/Utilities/Audio\ MIDI\ Setup.app` ，启动应用。
* 在列表中找到你的手机，然后点击 `Enable`按钮激活。
* 在终端运行 `ffmpeg -f avfoundation -list_devices true -i ""` ，在`AVFoundation audio devices`列表中找到手机的标识名字。这个标识使用 `:` 做为前缀。把这个标识作为 `audioInput` 的参数来调用 `mobile: startAudioRecording`。
* 测试你的配置是否生效。在手机里播放任意一个录音，然后在终端执行该命令：`ffmpeg -t 5 -f avfoundation -i ":1" -c:a aac -b:a 128k -ac 2 -ar 44100 -y ~/Desktop/out.mp4`（注意-i的参数值需要设置为上一步得到的值）。5秒后，在你的桌面就会有一个 `out.mp4` 文件，该文件录制了刚刚的语音。

苹果不允许电话录音重定向，所以你只能录制应用或者系统的声音。

###  拓展阅读

* https://github.com/appium/appium-xcuitest-driver/pull/1207
* https://www.macobserver.com/tips/quick-tip/iphone-audio-input-mac/
* http://www.lorisware.com/blog/2012/04/28/recording-iphone-emulator-video-with-sound/
