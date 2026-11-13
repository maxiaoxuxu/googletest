<!-- PAGE_ID: googletest_10_matchers -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([gtest-matchers.h:62-145](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-matchers.h#L62-L145))
- ([gtest-matchers.h:452-485](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-matchers.h#L452-L485))
- ([gmock-matchers.h:30-85](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-matchers.h#L30-L85))
- ([gmock-spec-builders.h:1643-1692](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1643-L1692))

</details>

# Matcher 匹配器机制

> **相关页面**：[断言与结果收集](./05_assertions_results.md) · [GoogleMock 运行时](./07_gmock_runtime.md) · [Expectation 匹配与调用约束](./08_expectations.md) · [Action 动作模型](./09_actions.md)

---

<!-- BEGIN:AUTOGEN googletest_10_matchers_main -->
## Matcher 匹配器机制

## Matcher 的接口

Matcher 的核心任务是“判断值是否满足条件”，并尽可能解释匹配结果。自定义 Matcher 实现 `MatcherInterface<T>::MatchAndExplain()`，同时提供 `DescribeTo()` / `DescribeNegationTo()`，让失败消息可以描述期望和实际值。([gtest-matchers.h:62-145](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest-matchers.h#L62-L145))

`MatchResultListener` 可接收匹配解释；没有人需要解释时，Matcher 可以避免构造额外诊断信息。([gtest-matchers.h:73-103](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest-matchers.h#L73-L103))

## Matcher<T> 的类型擦除和句柄

`Matcher<T>` 是可复制、不可变（除赋值外）的匹配器句柄，其实现持有 matcher 实例。使用模板与构造适配，调用点可以把值、具体 matcher 或自定义 matcher 转换为匹配器对象。([gtest-matchers.h:452-485](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gtest-matchers.h#L452-L485))

## 自定义 Matcher

gMock 提供 `MATCHER`、`MATCHER_P` 等宏，简化自定义匹配器的声明；匹配逻辑返回 bool，描述信息用于生成更可读的失败消息。([gmock-matchers.h:30-85](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gmock-matchers.h#L30-L85))

Matcher 同时被两条路径使用：

- `EXPECT_THAT(value, matcher)`：直接验证一个值。
- `EXPECT_CALL(mock, Method(matcher))`：在 Mock 方法调用时验证参数。

**源码推导**：Matcher 是“条件+解释”的对象，不是 Action；前者判断参数是否满足期望，后者定义匹配成功后的行为。

**Sources**：([gtest-matchers.h:62-145](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-matchers.h#L62-L145))、([gtest-matchers.h:452-485](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/include/gtest/gtest-matchers.h#L452-L485))、([gmock-matchers.h:30-85](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-matchers.h#L30-L85))、([gmock-spec-builders.h:1643-1692](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1643-L1692))
<!-- END:AUTOGEN googletest_10_matchers_main -->

---
