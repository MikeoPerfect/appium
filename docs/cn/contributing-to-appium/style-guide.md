## 给贡献者的风格指南

感谢您对Appium的贡献！以下是我们编写javascript代码时需要遵守的准则，请确认你的提交能符合这些规范，这有利于我们合并你的代码时能保持良好的编码风格。其中最核心的准则是：*使你的代码与其他代码的编码风格保持一致*。

### JavaScript

除了运行在设备上的代码（Android 使用[appium-uiautomator2-server](https://github.com/appium/appium-uiautomator2-server)，iOS 使用 [WebDriverAgent](https://github.com/appium/WebDriverAgent)）以外，Appium 用 [Node.js](https://nodejs.org/)编写，如果你对 JavaScript 不熟悉，请先学会 JavaScript 后再尝试修改代码。JavaScript 里有大量优秀、开源的资源（参考 [You Don't Know JavaScript](https://github.com/getify/You-Dont-Know-JS)）。

### 衍合（Rebasing）

每个 pull 请求中的提交（commits）都应该包含[逻辑变更(logical changes)](https://github.com/appium/appium/pull/920#issuecomment-21588553)。
如果有多位贡献者，请确保他们各自都有自己的提交记录，修改作者信息不是一个好主意。合并（merge）提交必须从 pull 请求中 rebase 。

### 检错（Linting）

所有代码都必须通过[ESLint](https://eslint.org/)的检查，你可以在 Appium 存储目录下，运行 `npm run lint` 来检查你的代码。相关配置都已在 [eslint-config-appium](https://github.com/appium/eslint-config-appium) 包里指定，现在大多数编辑器都集成了 ESLint，查看 [这里](https://eslint.org/docs/user-guide/integrations) 获取相关细节。

### 风格注释（Style notes）

我们使用了 JavaScript 的将来版本，因此需要使用 [Babel](https://babeljs.io/) 转换器进行渲染，这样当前版本的 [Node.js](https://nodejs.org/) 也能支持 新形式的 JavaScript.我们使用 [ES2015](https://babeljs.io/learn-es2015/)(旧称为 ES6)，ES2015 使用了一些尚未规范(not-yet-standard)的关键词 [async/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function).所有 Appium 贡献都必须遵循这份风格指南，幸好 linting 会帮助你严格执行这些规范。

*   使用两个空格来缩进, *不要使用 tabs*
*   在运算符两边，分别添加一个空格：

    ```js
    let x = 1;
    ```
    而不是
    ```js
    let x=1;
    ```

*   在列表（lists）,对象（objects）,函数调用（function calls）等语句块中，逗号和冒号后面需要添加一个空格：

    ```js
    let x = myFunc('lol', {foo: bar, baz: boo});
    ```
    而不是
    ```js
    let x = myFunc('lol',{foo:bar,baz:boo});
    ``

*   代码始终以分号结尾
*   左花括号应该和`function`,`if`等写在同一行，`else`应该被夹在两个花括号中间：

    ```js
    if (foo === bar) {
      // do something
    } else {
      // do something else
    }
    ```
    而不是
    ```js
    if (foo === bar)
    {
      // do something
    }
    else
    {
      // do something else
    }
    ```

*   `if`,`for`, 和`function`之后需要添加空格：

    ```js
    if (foo === bar) {
    ```
    ```js
    for (let i = 0; i < 10; i ++) {
    ```
    ```js
    let lol = function (foo) {
    ```
    而不是
    ```js
    if(foo === bar) {
    ```
    ```js
    for(let i = 0; i < 10; i ++) {
    ```
    ```js
    let lol = function(foo) {
    ```ol = function(foo) {
    ```

*   只有一行代码时，`if`语句块的花括号也应该添加上：

    ```js
    if (foo === bar) {
      foo++;
    }
    ```
    而不是
    ```js
    if (foo === bar)
      foo++;
    ```
    除了返回或报错后跳过(short-circuiting）
    ```js
    if (err) return;
    ```
    ```js
    if (err) throw new Error(err);
    ```

*   使用`===`, 而不是`==`；使用`!==`, 而不是`!=`，参考 [no surprises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
*   单行长度不应超过79个字符；
*   截断长字符串使用如下方法：

    ```javascript
    myFunc("This is a really long string that's longer " +
            "than 79 characters so I broke it up, woo");
    ```

*   注释需要和上一行代码左对齐：

    ```js
    if (foo === 5) {
      myFunc(foo);
      // foo++;
    }
    ```
    而不是
    ```js
    if (foo === 5) {
      myFunc(foo);
    //foo++;
    }
    ```

*   变量名应使用驼峰命名：

    ```js
    let myVariable = 42;
    ```
    而不是
    ```js
    let my_variable = 42;
    ```

*   使用 Appium 包： [appium-support](https://github.com/appium/appium-support)，检查是否有未定义的变量

    ```js
    util.hasValue(myVariable)
    ```

*   定义变量时，需要给定默认值：

    ```js
    let x = y || z;
    ```
    而不是
    ```js
    let x = y ? y : z;
    ```

### 测试代码风格（Test Style）:

使用 [mocha](https://mochajs.org/) 和 [chai](http://chaijs.com/)写测试代码，使用 [wd](https://github.com/admc/wd) WebDriver库。

在代码语义通顺和长度许可下，可以保持在同一行：

样例：

```js
driver.elementByTagName('el1').should.become('123');

driver
  .elementsByTagName('el1').should.eventually.have.length(0);
```

或者使用缩进来提高代码的可读性：

```js
driver
  .elementById('comments')
    .clear()
    .click()
    .keys('hello world')
    .getValue()
    .should.become('hello world')
  .elementById('comments')
    .getValue().should.become('hello world');

driver
  .execute("'NaN'--")
    .should.be.rejectedWith('status: 13');
```

本文由 [nicole1010](https://github.com/nicole1010) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。