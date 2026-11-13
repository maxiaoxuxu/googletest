<!-- PAGE_ID: googletest_06_test_variants -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([gtest-param-test.h:63-105](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-param-test.h#L63-L105))
- ([gtest-param-util.h:551-625](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/internal/gtest-param-util.h#L551-L625))
- ([gtest-typed-test.h:45-115](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-typed-test.h#L45-L115))
- ([gtest.h:2260-2345](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L2260-L2345))
- ([gtest-death-test.cc:1090-1160](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1090-L1160))
- ([gtest-death-test.cc:1172-1205](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1172-L1205))
- ([gtest.cc:6170-6260](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L6170-L6260))
- ([advanced.md:430-585](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/docs/advanced.md#L430-L585))

</details>

# 参数化、Typed、Death 与动态测试

> **相关页面**：[RUN_ALL_TESTS 执行路径](./03_execution.md) · [Fixture、Environment 与事件监听](./04_fixtures_environment.md) · [Expectation 匹配与调用约束](./08_expectations.md) · [构建与项目自测](./11_build_testing.md)

---

<!-- BEGIN:AUTOGEN googletest_06_test_variants_main -->
## 参数化、Typed、Death 与动态测试

## 值参数化测试

`TEST_P` 定义测试模式，`INSTANTIATE_TEST_SUITE_P` 提供一组参数生成器。常见生成器包括 `Range`、`Values`、`ValuesIn`、`Bool` 和 `Combine`。([gtest-param-test.h:63-105](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-param-test.h#L63-L105))

在真正执行前，`ParameterizedTestSuiteInfo::RegisterTests()` 遍历每个测试模式和每组实例化参数，为每个参数生成独立测试名，并调用 `MakeAndRegisterTestInfo()` 把它转成普通 TestInfo。因此，后续运行器不需要理解 TEST_P 的特殊语法。([gtest-param-util.h:551-625](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/internal/gtest-param-util.h#L551-L625)) ([gtest.cc:2848-2861](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L2848-L2861))

## Typed Test 与 Type-Parameterized Test

- **Typed Test**：将 Fixture 与一组类型关联，使用 `TYPED_TEST_SUITE` 和 `TYPED_TEST`。测试体通过 `TypeParam` 访问当前类型。([gtest-typed-test.h:45-85](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-typed-test.h#L45-L85))
- **Type-Parameterized Test**：先定义可复用的类型测试模式，后续再由不同实现实例化，适合检查多种实现是否满足同一个接口约定。([gtest-typed-test.h:85-115](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-typed-test.h#L85-L115))

## 动态注册

当宏声明不足以表达测试集合时，可以调用 `testing::RegisterTest()`，提供一个返回 Fixture 指针的 Factory。该接口必须在 `RUN_ALL_TESTS()` 前调用，注册结果最终仍进入同一 TestInfo/TestSuite 体系。([gtest.h:2260-2345](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L2260-L2345))

## Death Test

Death Test 检查进程是否按预期终止，以及退出状态和 stderr 是否匹配。源码提供两种主要风格：

| 风格 | 子进程行为 | 主要代价/优势 |
|---|---|---|
| `fast` | fork 后在子进程直接执行当前 death-test 语句 | 较快，但多线程 fork 环境风险更高 |
| `threadsafe` | 子进程重新执行测试程序，再通过内部参数只运行指定 death test | 更强调线程安全，启动开销更大 |

`NoExecDeathTest::AssumeRole()` 通过 pipe 和 fork 建立父子角色；`ExecDeathTest` 则使用重新执行的路径。([gtest-death-test.cc:1090-1160](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1090-L1160)) ([gtest-death-test.cc:1172-1205](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1172-L1205)) ([advanced.md:430-585](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/docs/advanced.md#L430-L585))

## Sharding

GoogleTest 可通过 total-shards 和 shard-index 控制进程分片。death-test 子进程会关闭常规 sharding，以避免指定 death test 在子进程中被分片过滤掉。([gtest.cc:6170-6260](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L6170-L6260))

**Sources**：([gtest-param-test.h:63-105](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-param-test.h#L63-L105))、([gtest-param-util.h:551-625](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/internal/gtest-param-util.h#L551-L625))、([gtest-typed-test.h:45-115](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-typed-test.h#L45-L115))、([gtest.h:2260-2345](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L2260-L2345))、([gtest-death-test.cc:1090-1160](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1090-L1160))、([gtest-death-test.cc:1172-1205](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest-death-test.cc#L1172-L1205))、([gtest.cc:6170-6260](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L6170-L6260))、([advanced.md:430-585](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/docs/advanced.md#L430-L585))
<!-- END:AUTOGEN googletest_06_test_variants_main -->

---
