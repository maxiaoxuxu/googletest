# GoogleTest / GoogleMock Wiki — 验证报告

- Repository: maxiaoxuxu/googletest
- Branch: test
- Frozen source commit: 5feffc24e4d6c49608d241d53cacb2c8143d2beb
- Plugin version: 2.0.13
- Locale / filename language: zh-CN
- Pages: 6
- New output: docs/wiki/_plugin_v2_0_13_zh_CN_full_validation/

## 页面生成状态

| Page | Scope | Status |
|---|---|---|
| 01_项目结构与构建总览.md | 项目结构与构建总览 | source reviewed |
| 02_聚合编译单元与测试入口.md | 聚合编译单元与测试入口 | source reviewed |
| 03_TEST宏与静态注册机制.md | TEST 宏与静态注册机制 | source reviewed |
| 04_RUN_ALL_TESTS执行链路.md | RUN_ALL_TESTS 执行链路 | source reviewed |
| 05_Fixture全局环境与事件报告.md | Fixture、全局环境与事件报告 | source reviewed |
| 06_GoogleMock集成与项目自测目标.md | GoogleMock 集成与项目自测目标 | source reviewed |

## 本轮发现的关键构建差异

- CMake gtest_main 编译 googletest/src/gtest_main.cc。
- 当前 test 分支的 Bazel //:gtest_main 编译 googlemock/src/gmock_main.cc。
- Bazel //:gtest 通过 glob 收集 GTest 与 GMock 普通实现源文件，并排除四个 aggregate/main .cc。
- CMake 的 GMock 在 MSVC 与非 MSVC 下使用不同的编译输入和链接关系。
- gtest-all.cc / gmock-all.cc 是实现源文件聚合，不是 main 程序入口。

## 验证状态

- Locale filename manifest: TOC declares zh-CN and all six page filenames use Chinese titles.
- Semantic source review: completed as a same-agent second pass; no independent subagent was available.
- Architecture coverage manifest: generated with per-page source inventory, claims, relationship IDs and diagram accounting. The manifest validator checks declared records; it does not prove source truth by itself.
- Cross-file source audit: not run against a local full checkout. GitHub connector source reads were performed, but the audit helper requires local source files to reopen line ranges and literal excerpts.
- Mermaid authoring lint for this run: not run locally.
- Mermaid.js parse/render or Mermaid CLI: not run.
- CMake configure/build, Bazel build/test, CTest: not run.

## Validation interpretation

This is a source-grounded Wiki generation and second-pass review, not a successful build/test report. Renderer and project-build statuses remain not_run; they are not silently converted to passed. The plugin package's separate unit-test suites passed before this repository run (45 architecture/filename/version tests and 10 Mermaid static-lint tests); those tests validate plugin logic, not this GoogleTest project's binaries.
