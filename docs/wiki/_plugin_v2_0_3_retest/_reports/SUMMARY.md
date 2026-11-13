# DeepWiki 2.0.3 插件复测报告

## 测试范围

- 目标仓库：`maxiaoxuxu/googletest`
- 写入分支：`test`
- 源码基准：`main @ a8380b01a25ebdb130097b607b3afed2a58d04ba`
- 插件 Skill：`deepwiki-codebase-wiki / deepwiki-wiki`，由本轮用户显式 @mention 后加载
- 输出：`docs/wiki/_plugin_v2_0_3_retest/`
- 范围：复测两篇已有页面（TEST 注册、GoogleMock Expectation），不是 11 页全量重生成

## 阶段执行情况

| 阶段 | 状态 | 说明 |
|---|---|---|
| repo-scan | 完成（GitHub Connector fallback） | 读取递归文件树、仓库元数据和指定源码；没有本地工作树，未运行原始 collect_context.py |
| toc-design | 完成 | 基于现有 Wiki 主题，构造隔离的两页复测 TOC |
| doc-write | 完成（sequential fallback） | 两个页面分别按独立 page_id 生成；当前宿主未暴露原生 Subagent 调度工具 |
| validate-docs | 完成（静态） | PAGE_ID、AUTOGEN、H1、TOC、源码引用 commit 和行号范围检查 |
| doc-summary | 完成 | 本报告 |
| incremental-sync | 未运行 | 本轮是隔离复测，不是增量同步 |

## 与原页面对比

### 02_registration.md

- 原版重点说明 TEST 宏生成类、静态注册、TestInfo/UnitTestImpl/TestSuite 分工和 Factory。
- 复测版把“注册阶段”和“执行阶段”明确拆开，沿 `GTEST_TEST_` → 静态 `test_info_` → `MakeAndRegisterTestInfo` → `UnitTestImpl::AddTestInfo` → `TestSuite::AddTestInfo` → `TestInfo::Run` → Factory 创建 Fixture 的完整链路展开。
- 增加了参数化测试单独注册展开的边界说明，避免将普通 TEST/TEST_F 流程过度泛化。

### 08_expectations.md

- 原版已经解释 EXPECT_CALL/ON_CALL、反向查找、调用计数、前置依赖和饱和行为。
- 复测版进一步补充 `ShouldHandleArguments()` 的真实条件（未退休、前置期望满足、参数 matcher 匹配），并引用实现而不只引用声明。
- 明确区分锁内完成匹配/状态更新与锁外执行用户 Action，解释这样做是为了避免用户回调重入导致死锁。
- 将调用时的 unexpected/excessive call 与后续校验时的 unmet expectation 区分。

**质量判断**：两篇复测版在执行路径完整性、源码证据颗粒度和事实/推导边界上比原版更好；这是一轮两页定向质量复测，不能据此声称全部 11 页都已改善。

## 静态校验

- 页面：2/2
- PAGE_ID：2/2 正确且唯一
- AUTOGEN：2/2 配对
- H1：2/2 各一个
- Mermaid：复测副本 2 个图块；另对原始 Wiki 11 页、冒烟测试 2 页和复测页 2 页共 9 个 Mermaid 块做静态审计。发现原始 08 与复测 08 都采用 quoted pipe-edge-label 写法；复测副本已修正。详见 `MERMAID_AUDIT.md`。
- 源码引用：均固定到同一不可变 commit；行号范围均未超出对应源文件行数
- 结构错误：0

## 未执行项

- 没有 Mermaid.js 浏览器 parse/render；没有生成或检查浏览器运行时 SVG。
- 没有 Mermaid CLI。
- 没有原始 Python helper 脚本执行（当前没有目标仓库本地工作树/脚本执行环境）。
- 没有 Subagent 并行；本轮是顺序执行。
- 没有运行 CMake build / CTest。

## 产物与保护

- 原有 `docs/wiki/` 11 页及原有两页冒烟测试备份均未覆盖。
- 本轮新增内容全部位于 `docs/wiki/_plugin_v2_0_3_retest/`。
- `main` 未写入。

## 后续 Mermaid 审计补充

- 根因定位到插件源规则：`.apm/skills/wiki/references/mermaid_policy.md` 将 `A -->|\"Yes\"| B` 作为边标签正确示例，静态检查未拦截该模式。
- 本轮只修正 `_plugin_v2_0_3_retest/08_expectations.md`，没有覆盖原始 Wiki，也没有修改插件源仓库。
- 新增全量静态审计：[`MERMAID_AUDIT.md`](./MERMAID_AUDIT.md)。
- Mermaid.js/CLI 真实渲染尚未执行；不能将其描述为通过。
