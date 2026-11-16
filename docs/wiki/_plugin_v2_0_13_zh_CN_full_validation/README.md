# GoogleTest / GoogleMock 源码 Wiki（DeepWiki 2.0.13 验证）

- Repository: maxiaoxuxu/googletest
- Branch: test
- Frozen source commit: 5feffc24e4d6c49608d241d53cacb2c8143d2beb
- Rule baseline: DeepWiki Codebase Wiki 2.0.13
- Locale / filename language: zh-CN
- Output directory: docs/wiki/_plugin_v2_0_13_zh_CN_full_validation/

## 页面

- [项目结构与构建总览](01_项目结构与构建总览.md)
- [聚合编译单元与测试入口](02_聚合编译单元与测试入口.md)
- [TEST 宏与静态注册机制](03_TEST宏与静态注册机制.md)
- [RUN_ALL_TESTS 执行链路](04_RUN_ALL_TESTS执行链路.md)
- [Fixture、全局环境与事件报告](05_Fixture全局环境与事件报告.md)
- [GoogleMock 集成与项目自测目标](06_GoogleMock集成与项目自测目标.md)

## 本轮重点

本轮重点复核“聚合编译单元与测试入口”，把聚合 .cc、构建 target、程序入口三个层面分开。特别记录当前 test 分支中：
- CMake 的 gtest_main 编译 googletest/src/gtest_main.cc。
- Bazel 的 //:gtest_main 编译 googlemock/src/gmock_main.cc。
- Bazel 的 //:gtest glob 收集 GoogleTest 与 GoogleMock 普通实现 .cc，并排除四个 aggregate/main .cc。
- CMake 的 GMock 在 MSVC / 非 MSVC 下采用不同编译输入和链接关系。

## 运行说明

本轮在当前会话中通过 GitHub 源码接口读取固定 commit，按 DeepWiki 2.0.13 的 TOC、中文文件名、PAGE_ID/AUTOGEN、架构关系图和覆盖报告规则组织验证产物。当前会话没有可直接调用已安装插件运行时的执行入口，因此这组文件用于验证规则/产物契约与源码分析质量，**不能冒称为一次插件运行时自动执行记录**。

本目录是独立的新验证 run，不覆盖 docs/wiki/ 中已有页面、根目录文件或历史 run。
