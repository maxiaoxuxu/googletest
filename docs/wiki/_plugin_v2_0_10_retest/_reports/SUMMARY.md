# DeepWiki 2.0.10 — GoogleTest 执行生命周期定向回归

## 基本信息
- 仓库：`maxiaoxuxu/googletest`
- 分支：`test`
- 文档源码基准：`277cfa07d637aac85a388d1cb0c6adb585a1432e`
- 本次写入前 test 分支 HEAD：`d5221cb46dcdce2711e9e429291602dfdc84c9ec`
- 输出目录：`docs/wiki/_plugin_v2_0_10_retest/`
- 页面：`03_test_execution_lifecycle.md`
- 执行策略：当前宿主无可观察原生 Subagent 接口，采用 sequential fallback

## 跨文件核对
- 通过 GitHub connector 按冻结 commit 重新读取 5 个源文件，并逐项核对页面 Markdown、TOC、architecture map 和 coverage report。
- 核对 6 条 claims、31 条 relationships、全部 evidence 行范围与 `contains` 片段、57 个源码引用出现位置、3 个 DIAGRAM_ID 与 3 张 Mermaid 图，以及所有图关系片段/正文锚点。
- 本轮 connector-backed 核对结果：**0 个跨文件不一致项**。没有本地 GoogleTest checkout，因此未声称执行了 `audit_wiki.py` 的本地 CLI。

## 分析范围
- TEST/TEST_F 静态注册到 TestInfo / TestSuite
- main → InitGoogleTest → PostFlagParsingInit
- RUN_ALL_TESTS → UnitTest::Run → UnitTestImpl::RunAllTests
- Global Environment → TestSuite → TestInfo → Test fixture
- SetUp / TestBody / TearDown 的条件和清理顺序
- Assertion result → TestResult → TestEventListener → result printer
- fail-fast、skip、global/suite/test setup 失败分支

## 覆盖清单
- 源码文件：5
- claims：6
- 关键关系：31
- Mermaid 图：3
- 每张图都有 DIAGRAM_ID，并有一一对应 diagram audit。
- 每条关系都含源文件路径、行范围、contains 片段和 Markdown 表示位置。
- 正文源引用固定到同一源码 SHA。

## 重要分析结论
- 常规 TEST/TEST_F 静态注册发生在 main() 之前，并非运行时扫描测试目录。
- 参数化测试由 PostFlagParsingInit() 注册。
- 全局 Environment、TestSuite、单个 Test fixture 是不同生命周期层级。
- Test::TearDown 用于尽可能清理，即使 setup 或 TestBody 失败也会执行。
- Listener 开始类和结束类通知的派发顺序并不相同；结束回调有逆序转发逻辑。

## 校验边界
- 页面结构、引用 SHA、DIAGRAM_ID、图数量和 coverage ledger 已随产物提供并完成 connector-backed 跨文件核对。
- 真正的跨文件自动校验需要在有 GoogleTest 本地源码工作树的环境运行 `audit_wiki.py`；当前会话用 GitHub connector 读取源码，不能声称在本会话完整运行了该工具。
- Mermaid.js parse/render：not_run。
- CMake configure/build/CTest：not_run。
- 本页是源代码级生命周期分析，不是 GoogleTest 运行或编译测试。

## 文件
- `toc.yaml`
- `03_test_execution_lifecycle.md`
- `_context/architecture_map.json`
- `_reports/architecture_coverage.json`
- `_reports/SUMMARY.md`
