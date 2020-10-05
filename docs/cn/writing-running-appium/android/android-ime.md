## 如何模拟IME动作生成

Android开发人员经常使用带有`actionId`参数的[onEditorAction](https://developer.android.com/reference/android/widget/TextView.OnEditorActionListener.html#onEditorAction(android.widget.TextView, int, android.view.KeyEvent))回调来实现动作处理，例如，在屏幕键盘上按下`Search`或`Done`按钮的时候。从1.9.2以后版本的Appium允许通过提供特殊`mobile:`命令来自动生成此类动作。

### mobile: performEditorAction

对当前关注的元素执行给定的编辑器动作。

#### 支持的参数

- *action*：待执行的编辑器动作的名称或整数代码。支持以下操作名称：`normal, unspecified, none, go, search, send, next, done, previous`。阅读https://developer.android.com/reference/android/view/inputmethod/EditorInfo了解有关此主题的更多详细信息。

#### 用法示例

```java
// Java
driver.executeScript("mobile: performEditorAction", ImmutableMap.of("action", "Go"));
```

#### 用法示例

```python
# Python
driver.execute_script('mobile: performEditorAction', {'action': 'previous'})
```

