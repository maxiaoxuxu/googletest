# DeepWiki 2.0.9 — GoogleTest 架构完整性回归测试

## 基本信息
- 目标仓库：`maxiaoxuxu/googletest`
- 目标分支：`test`
- 源码基准：`277cfa07d637aac85a388d1cb0c6adb585a1432e`
- 输出目录：`docs/wiki/_plugin_v2_0_9_retest/`
- 测试范围：单页定向回归，专门覆盖上一轮发现的“正文提到 gmock_main，但架构图遗漏入口”问题
- 执行策略：当前宿主没有可观察的原生 Subagent 接口，本轮按单页顺序执行

## 执行边界
本轮是依据 DeepWiki 源码分支中的 Skill、reference 和校验器规则完成的 connector-backed 定向回归，不是通过当前已安装的 2.0.9 release 包直接启动插件运行时。当前安装包 2.0.9 的发布时间早于源分支最新提交，两个产物的文件内容尚未同步；因此本报告证明的是源分支规则与覆盖清单的回归结果，不证明已安装包已包含这些最新修复。

## 本轮修正
- 将原来混在一起的编译输入、链接依赖、运行入口拆成两张图。
- 构建图明确画出 gtest/gmock targets 的 compile input 与 link dependency。
- 运行入口图明确画出 gtest_main 与 gmock_main 两条普通平台路径。
- 增加 Arduino、QuRT、Windows Mobile 的条件入口表。
- 将 MSVC 与非 MSVC 的 GoogleMock target 组成分开表达。

## 架构覆盖校验
- 源码文件：6 个
- 关键关系：20 条
- Mermaid 图：2 张
- 每张图均有独立 diagram audit，并在 Markdown 中用 `DIAGRAM_ID` 标记与报告一一对应。
- 关键关系缺失、证据缺失、未审阅源文件和图内遗漏由 coverage manifest 校验器检查。
- 当前 manifest 校验结果：**passed**（1 page，20 relationships，2 diagrams，0 errors，0 incomplete，0 warnings）。
- 负向回归：从 runtime diagram 中移除 `rel-gmock-entry` 后，校验器按预期返回 **failed / critical_diagram_omission**。
- Mermaid 静态 authoring-style spot-check：2 个 Mermaid fence，quoted pipe-label findings 为 0。此项不是 Mermaid.js parser/render。

注意：校验器验证的是已声明的 coverage manifest；它不能自动发现 architecture map 自身漏掉的关系。因此本轮另外重新打开 CMakeLists、gtest-all.cc、gmock-all.cc、gtest_main.cc、gmock_main.cc 进行了同一 Agent 的第二遍源码核对。

## Mermaid 与运行时边界
- 两张图使用明确的 edge label 区分 compile input、link dependency、entrypoint 和 initialization。
- Mermaid.js 浏览器 parse/render：`not_run`。
- Mermaid CLI：`not_run`。
- CMake configure/build/CTest：`not_run`。
- 本轮不声称实际编译或执行了 GoogleTest。

## 文件
- `toc.yaml`
- `02_aggregate_units.md`
- `_context/architecture_map.json`
- `_reports/architecture_coverage.json`
- `_reports/SUMMARY.md`

本轮是单页定向回归，不是完整仓库 Wiki 重生成。
