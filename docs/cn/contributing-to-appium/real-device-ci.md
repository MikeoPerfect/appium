# 在真机上持续集成

Appium 使用 [TestObject](https://testobject.com/) 服务，在真机上运行自动化功能测试。

## How it works

* TestObject 如何执行 Appium 测试，可以查看[这里](https://help.testobject.com/docs/tools/appium/reference/) 获取详细信息
* 使用 [wd](https://github.com/admc/wd)的测试脚本，需要从 `appium-test-support` 导入方法 `enableTestObject` 来运行 TestObject 测试 ，
这个方法会在测试执行前被调用。
* 这个方法做了以下事情:
  * 拉取 appium 并在 shell 里运行 git 命令 clone 下来
  * 需要要测试的 driver 版本，指向某个代码提交的 git 链接
  * 安装 npm 模块
  * 压缩文件夹
  * 上传到 S3
  * 重写 wd 以便能加上 testobject 特定的 desired capabilities，包括 S3 url路径

## 环境

* 设置环境变量
  * AWS_ACCESS_KEY_ID: 有 S3 访问权限的 ID
  * AWS_SECRET_ACCESS_KEY
  * AWS_REGION
  * AWS_S3_BUCKET: 写入的 bucket 名 
  * TESTOBJECT_API_KEY

## 范例

```javascript
// This script, if run before the rest of the tests, will use TestObject appium staging server
import { enableTestObject, disableTestObject } from 'appium-test-support';
import wd from 'wd';
import { startServer, DEFAULT_PORT } from '../../..';
import logger from '../../../lib/logger';

if (process.env.TESTOBJECT_E2E_TESTS) {
  logger.debug('Running tests on TestObject');

  let wdObject;
  before(async function () {
    // Use a commit SHA as the git branch
    const branch = process.env.COMMIT_HASH || process.env.TRAVIS_COMMIT;
    if (!branch) {
      throw new Error(`A commit must be provided in $COMMIT_HASH`);
    }
    // Uploads the zip and injects 'appium-uiautomator2-driver' as the branch
    wdObject = await enableTestObject(wd, 'appium-uiautomator2-driver', `git@github.com:appium/appium-uiautomator2-driver.git#${branch}`);
  });
  after(async function () {
    // Reverses the overriding of 'wd'
    await disableTestObject(wdObject);
  });

} else {
  before(async function () {
    // If we're not using TestObject, we're using a local server
    await startServer(DEFAULT_PORT, 'localhost');
  });
}

```

本文由 [nicole1010](https://github.com/nicole1010) 翻译