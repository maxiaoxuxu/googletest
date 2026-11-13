# GoogleTest / GoogleMock 源码 Wiki

源码基准：[`a8380b01a25ebdb130097b607b3afed2a58d04ba`](https://github.com/maxiaoxuxu/googletest/commit/a8380b01a25ebdb130097b607b3afed2a58d04ba)，固定读取目标仓库 `main` 的该提交，生成内容写在 `test` 分支。

## 阅读顺序

1. [项目总览与模块边界](01_project_overview.md)
2. [TEST 宏与测试注册](02_registration.md)
3. [RUN_ALL_TESTS 执行路径](03_execution.md)
4. [Fixture、Environment 与事件监听](04_fixtures_environment.md)
5. [断言与结果收集](05_assertions_results.md)
6. [参数化、Typed、Death 与动态测试](06_test_variants.md)
7. [GoogleMock 运行时](07_gmock_runtime.md)
8. [Expectation 匹配与调用约束](08_expectations.md)
9. [Action 动作模型](09_actions.md)
10. [Matcher 匹配器机制](10_matchers.md)
11. [构建与项目自测](11_build_testing.md)

## 生成记录

- TOC：[`toc.yaml`](toc.yaml)
- 阶段上下文：[`_context/context_pack.json`](_context/context_pack.json)
- 校验：[`_reports/structure_validation.json`](_reports/structure_validation.json)、[`_reports/mermaid_invalid.json`](_reports/mermaid_invalid.json)
- 汇总：[`_reports/SUMMARY.md`](_reports/SUMMARY.md)

> 本 Wiki 用于源码学习和架构定位。版本、API 和实现行为均应以本 Wiki 所固定的 commit 为准，不应将 `main` 后续变化自动套用到本文档。
