# GoogleTest / GoogleMock Wiki — 验证报告

- Repository: maxiaoxuxu/googletest
- Branch: test
- Frozen source commit: 5feffc24e4d6c49608d241d53cacb2c8143d2beb
- Rule baseline: DeepWiki Codebase Wiki 2.0.13
- Locale / filename language: zh-CN
- Pages: 6
- Mermaid diagrams: 6
- Declared architecture relationships: 39
- Source citations: 38
- Exact source excerpts checked: 50 / 50
- New output: docs/wiki/_plugin_v2_0_13_zh_CN_full_validation/

## 关键结论

- CMake gtest_main 编译 googletest/src/gtest_main.cc。
- 当前 test 分支的 Bazel //:gtest_main 编译 googlemock/src/gmock_main.cc。
- Bazel //:gtest 通过 glob 收集 GTest 与 GMock 普通实现源文件，并排除四个 aggregate/main .cc。
- CMake 的 GMock 在 MSVC 与非 MSVC 下采用不同的编译输入与链接组织。
- gtest-all.cc / gmock-all.cc 是实现源文件聚合，不是 main 程序入口。
- 常规 TEST / TEST_F 的静态注册发生在 main() 之前；参数化测试实例另由 PostFlagParsingInit() 注册。
- RUN_ALL_TESTS() 仅转到 UnitTest::Run()；实际调度位于 UnitTestImpl::RunAllTests() 及其下游。

## 本轮结构与证据检查

| 检查项 | 结果 | 说明 |
|---|---|---|
| TOC locale / filename | passed | 声明 zh-CN，6 个页面文件名均使用中文标题 |
| Page identity / diagram markers | passed | 6/6 页具有匹配 PAGE_ID，每页 1 个 DIAGRAM_ID |
| Map / coverage relationship IDs | passed | 两份清单的 39 条关系 ID 对齐 |
| Mermaid relation fragments | passed | 图中代表的边片段均能在对应图体中找到 |
| Source citation baseline | passed | 页面引用均固定到 5feffc24e4d6c49608d241d53cacb2c8143d2beb |
| Exact source excerpts | passed | 通过 GitHub 源码读取逐条核验 50 个 path/line/contains 摘录，全部命中 |
| Quoted pipe-label rule | passed | 6 个 Mermaid 图中未发现带引号的 pipe-edge label |
| Architecture review | completed | 同一 agent 第二轮回读关键源码；不是独立 agent 审核 |

## 仍未执行的检查

- 官方本地 helper：本次没有在完整本地 checkout 上运行 validate_toc_filenames.py、validate_coverage.py、audit_wiki.py。上表列出的是本轮对同一结构约束和源码摘录所做的接口侧检查结果，不将其伪装成 helper 的执行日志。
- Cross-file audit helper：not_run。audit_wiki.py 需要本地完整源码目录，当前会话通过 GitHub connector 读源码，没有完成完整本地 checkout。
- Mermaid.js parse/render 或 Mermaid CLI：not_run。静态边标签规则通过不代表渲染器解析通过。
- CMake configure/build、Bazel build/test、CTest：not_run。本报告是源码架构分析，不是项目构建/测试通过报告。

## 插件运行时边界

当前会话没有能够直接调用已安装 DeepWiki 插件运行时的工具入口。本次验证目录是通过 GitHub 源码接口读取固定提交、遵循 DeepWiki 2.0.13 的产物规则生成和复核的；它证明规则和输出契约可以被落实，但**不作为“插件运行时已被自动触发并完成一次生成”的证据**。要验证真正的插件运行时，需要在支持调用该插件的 ChatGPT 会话中直接发起一次生成任务。

## 插件包自身测试（与 GoogleTest 项目测试区分）

插件包本轮更新前后运行的测试结果为：
- Architecture / filename / version auditor tests: 45 passed.
- Mermaid static-lint tests: 10 passed.

以上是插件工具代码测试，不是 GoogleTest 项目的 CMake/Bazel/CTest 结果。
