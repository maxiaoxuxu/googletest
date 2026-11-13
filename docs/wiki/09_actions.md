<!-- PAGE_ID: googletest_09_actions -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([gmock-actions.h:700-765](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-actions.h#L700-L765))
- ([gmock-actions.h:850-950](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-actions.h#L850-L950))
- ([gmock-spec-builders.h:1140-1218](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1140-L1218))
- ([gmock-spec-builders.h:1730-1845](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1730-L1845))

</details>

# Action 动作模型

> **相关页面**：[GoogleMock 运行时](./07_gmock_runtime.md) · [Expectation 匹配与调用约束](./08_expectations.md) · [Matcher 匹配器机制](./10_matchers.md)

---

<!-- BEGIN:AUTOGEN googletest_09_actions_main -->
## Action 动作模型

## Action 把“调用时做什么”抽象出来

`ActionInterface<F>` 定义虚函数 `Perform()`，允许动作拥有状态或副作用。外层 `Action<R(Args...)>` 是可复制的句柄，内部通过共享指针持有 ActionInterface 实现。([gmock-actions.h:700-765](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gmock-actions.h#L700-L765))

这使得期望匹配和具体行为解耦：Expectation 决定何时触发哪个 Action，Action 决定触发后如何产生返回值或副作用。

## 多态 Action

`PolymorphicAction` 可以把一个泛型实现转换成具体函数签名对应的 Action。实现类提供模板化的 `Perform<Result>()`，框架再用适配类包装成 ActionInterface。([gmock-actions.h:850-900](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gmock-actions.h#L850-L900))

## Return 与一次性动作

`Return(value)` 是常见动作。源码中的 ReturnAction 会根据目标返回类型做类型约束和转换；对仅允许执行一次、需要 move 语义的情况，代码还提供 OnceAction 路径。([gmock-actions.h:919-950](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gmock-actions.h#L919-L950))

## WillOnce / WillRepeatedly 的选择

Expectation 会保存一组一次性 Action 和一个重复 Action。按匹配调用次数，框架优先取对应的 WillOnce；超过一次性动作数量后再取 WillRepeatedly。若没有重复动作而一次性动作耗尽，会触发相应的诊断。([gmock-spec-builders.h:1140-1218](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/gmock-spec-builders.h#L1140-L1218))

**源码推导**：Action 不负责匹配参数，也不决定调用是否允许发生；这些责任属于 Matcher 和 Expectation。Action 只负责已匹配调用的行为。

**Sources**：([gmock-actions.h:700-765](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-actions.h#L700-L765))、([gmock-actions.h:850-950](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-actions.h#L850-L950))、([gmock-spec-builders.h:1140-1218](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1140-L1218))、([gmock-spec-builders.h:1730-1845](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/include/gmock/gmock-spec-builders.h#L1730-L1845))
<!-- END:AUTOGEN googletest_09_actions_main -->

---
