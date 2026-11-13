<!-- PAGE_ID: googletest_05_assertions_results -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([primer.md:100-146](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/docs/primer.md#L100-L146))
- ([gtest.h:398-448](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L398-L448))
- ([gtest.cc:2501-2525](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L2501-L2525))
- ([gtest-test-part.cc:35-75](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-test-part.cc#L35-L75))

</details>

# 断言与结果收集

> **相关页面**：[RUN_ALL_TESTS 执行路径](./03_execution.md) · [Fixture、Environment 与事件监听](./04_fixtures_environment.md) · [Matcher 匹配器机制](./10_matchers.md)

---

<!-- BEGIN:AUTOGEN googletest_05_assertions_results_main -->
## 断言与结果收集

## EXPECT 与 ASSERT：失败控制流不同

两类宏都用于表达断言，但失败时对当前函数的影响不同：

| 宏族 | 失败结果 | 当前测试函数 |
|---|---|---|
| `EXPECT_*` | 非致命失败 | 继续执行，因此可累计多个失败 |
| `ASSERT_*` | 致命失败 | 立即从当前函数返回 |

因此，检查彼此独立的多个条件时通常使用 EXPECT；若后续代码必须依赖当前条件成立，则使用 ASSERT，避免在无效状态下继续执行。([primer.md:100-146](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/primer.md#L100-L146))

## 断言如何形成结果记录

框架把断言结果表示为 TestPartResult。它区分成功、跳过、致命失败和非致命失败；TestPartResultArray 提供追加与按索引读取。([gtest-test-part.cc:35-75](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest-test-part.cc#L35-L75))

`TestResult` 汇总一条测试执行中的 TestPartResult，并提供 `Passed()`、`Skipped()`、`Failed()`、`HasFatalFailure()` 等查询。([gtest.h:398-448](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.h#L398-L448)) ([gtest.cc:2501-2525](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L2501-L2525))

## 结果层级

- TestInfo 持有单项测试的结果。
- TestSuite 还持有 suite 级 ad hoc result，用于 suite SetUp/TearDown 等上下文。
- 全局执行器最终根据 suite 和程序级结果决定 `RUN_ALL_TESTS()` 的返回值。([gtest.h:534-620](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.h#L534-L620)) ([gtest.h:670-800](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.h#L670-L800)) ([primer.md:341-379](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/primer.md#L341-L379))

## 退出码是 CI 的判定依据

`RUN_ALL_TESTS()` 成功返回 0，失败返回 1；默认 main 直接将其作为进程退出码。CI 应依据退出码判定，而不能只解析 stdout 中的文字。([primer.md:341-379](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/primer.md#L341-L379)) ([gtest_main.cc:53-65](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest_main.cc#L53-L65))

**Sources**：([primer.md:100-146](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/docs/primer.md#L100-L146))、([gtest.h:398-448](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L398-L448))、([gtest.cc:2501-2525](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L2501-L2525))、([gtest-test-part.cc:35-75](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-test-part.cc#L35-L75))
<!-- END:AUTOGEN googletest_05_assertions_results_main -->

---
