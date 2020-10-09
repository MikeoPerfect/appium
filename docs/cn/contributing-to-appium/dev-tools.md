## Appium 开发命令

每个 Appium 包都包含大量用于自动化开发任务的 NPM 脚本：

| 任务             | 描述                                            |
|------------------|--------------------------------------------------------|
| npm run build    | 代码转译到 `build` 目录下                                 |
| npm run lint     | 运行 ESLint                                             |
| npm run test     | 清理，审查，转译以及运行单元测试                             |
| npm run e2e-test | 转译并运行功能测试                                        |
| npm run watch    | 代码更改后自动执行 `test` 命令                             |
| npm run mocha    | 执行 `mocha` 测试                                        |

此外，Appium 主包有个`npm generate-docs`任务，可以生成命令文档。

（翻译说明，以上命令均可在 package.json 文件中查看：
"build": "gulp transpile",
"test": "gulp once",
"e2e-test": "gulp e2e-test",
"watch": "gulp watch",
"generate-docs": "node ./build/commands-yml/parse.js"）

本文由 [nicole1010](https://github.com/nicole1010) 翻译，由 [lihuazhang](https://github.com/lihuazhang) 校验。