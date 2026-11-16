# GoogleTest / GoogleMock 源码 Wiki（插件 2.0.13 验证）

- Repository: maxiaoxuxu/googletest
- Branch: test
- Frozen source commit: 5feffc24e4d6c49608d241d53cacb2c8143d2beb
- Plugin: DeepWiki Codebase Wiki 2.0.13
- Locale: zh-CN
- Output: docs/wiki/_plugin_v2_0_13_zh_CN_full_validation/

## 页面

- [项目结构与构建总览](01_项目结构与构建总览.md)
- [聚合编译单元与测试入口](02_聚合编译单元与测试入口.md)
- [TEST 宏与静态注册机制](03_TEST宏与静态注册机制.md)
- [RUN_ALL_TESTS 执行链路](04_RUN_ALL_TESTS执行链路.md)
- [Fixture、全局环境与事件报告](05_Fixture全局环境与事件报告.md)
- [GoogleMock 集成与项目自测目标](06_GoogleMock集成与项目自测目标.md)

## 本轮重点

重点复核“聚合编译单元与测试入口”，把聚合 .cc、构建 target、程序入口三个层面拆开。另行审计 CMake 与 Bazel 的差异，特别是 Bazel //:gtest_main 使用 googlemock/src/gmock_main.cc，而 CMake gtest_main 使用 googletest/src/gtest_main.cc。

## 产物

- toc.yaml：本次页面目录和 zh-CN 文件名声明
- _context/architecture_map.json：页面映射的源码文件与关系
- _reports/architecture_coverage.json：逐页声明的证据与图关系覆盖
- _reports/SUMMARY.md：验证状态和边界

本目录是独立的新验证 run，不覆盖 docs/wiki/ 中已有页面和历史 run。
