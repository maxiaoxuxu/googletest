<!-- PAGE_ID: googletest_04_fixtures_environment -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([gtest.h:247-340](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L247-L340))
- ([gtest.cc:2766-2786](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L2766-L2786))
- ([gtest.cc:3055-3125](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L3055-L3125))
- ([gtest.cc:6030-6095](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L6030-L6095))

</details>

# Fixture、Environment 与事件监听

> **相关页面**：[RUN_ALL_TESTS 执行路径](./03_execution.md) · [断言与结果收集](./05_assertions_results.md) · [参数化、Typed、Death 与动态测试](./06_test_variants.md)

---

<!-- BEGIN:AUTOGEN googletest_04_fixtures_environment_main -->
## Fixture、Environment 与事件监听

## 单个测试的 Fixture 生命周期

`TEST_F(Fixture, Name)` 生成的类以 Fixture 为父类。每次运行某个测试时都会创建一个新的 Fixture 实例；单项测试流程是：

1. 构造 Fixture。
2. 调用 `SetUp()`。
3. 如果 SetUp 没有产生 fatal failure 或 skip，则执行 `TestBody()`。
4. 无论 SetUp 或 TestBody 是否失败，仍尝试调用 `TearDown()`。
5. 析构 Fixture。

这一顺序由 `Test::Run()` 和 `TestInfo::Run()` 实现。([gtest.cc:2766-2786](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L2766-L2786)) ([gtest.cc:2897-2935](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L2897-L2935))

## Suite 级资源

如果多个测试要共享昂贵资源，可以使用静态 `SetUpTestSuite()` / `TearDownTestSuite()`。它们分别在 suite 中第一个测试执行前和最后一个测试执行后调用。([gtest.h:247-268](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.h#L247-L268)) ([gtest.cc:3055-3125](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L3055-L3125))

需要注意：suite 级资源共享不等于共享每个测试的 Fixture 对象。Fixture 对象仍然是一条测试一次。

## 全局 Environment

`testing::Environment` 可把测试程序级的准备/清理放在 suite 遍历之外。当前 `RunAllTests()` 会在迭代开始时设置 Environment，在 suite 执行结束后反向清理；repeat 模式还可控制是否每轮重新创建环境。([gtest.cc:6030-6095](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L6030-L6095))

## 事件监听器

执行器在程序、迭代、suite 和单个测试的边界发出事件通知。自定义 listener 可以在不改测试代码的情况下接入日志、报告和外部集成。TestInfo 执行前后会触发 `OnTestStart` / `OnTestEnd`。([gtest.cc:2897-2935](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L2897-L2935)) ([gtest.cc:3055-3125](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest.cc#L3055-L3125))

**Sources**：([gtest.h:247-340](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest.h#L247-L340))、([gtest.cc:2766-2786](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L2766-L2786))、([gtest.cc:3055-3125](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L3055-L3125))、([gtest.cc:6030-6095](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest.cc#L6030-L6095))
<!-- END:AUTOGEN googletest_04_fixtures_environment_main -->

---
