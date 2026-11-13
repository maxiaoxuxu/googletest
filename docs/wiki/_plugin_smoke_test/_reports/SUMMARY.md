# Wiki 冒烟测试报告

- **插件版本**：deepwiki-codebase-wiki 2.0.2
- **目标仓库**：`maxiaoxuxu/googletest`
- **目标分支**：`test`
- **源码基准**：`main @ a8380b01a25ebdb130097b607b3afed2a58d04ba`
- **输出目录**：`docs/wiki/_plugin_smoke_test/`
- **生成页面**：2

## 阶段状态

| 阶段 | 状态 | 说明 |
|---|---|---|
| repo-scan | completed with connector fallback | 使用 GitHub recursive tree 与定向文件读取；未执行本地 collect_context.py |
| toc-design | completed | 创建 2 页 TOC，源文件映射到实际存在的 CMake 与聚合编译文件 |
| doc-write | completed, sequential fallback | 两页独立生成；没有可观察的原生 Subagent 并行接口 |
| validate-docs | completed, static | PAGE_ID、AUTOGEN、H1、TOC 和引用格式检查通过 |
| doc-summary | completed | 本报告基于 TOC、页面和静态校验结果生成 |
| incremental-sync | not run | 本轮为全新输出目录，不是增量更新 |

## 输出

- `toc.yaml`
- `01_build_graph.md`
- `02_aggregate_units.md`
- `README.md`
- `_context/context_pack.json`
- `_reports/structure_validation.json`
- `_reports/mermaid_invalid.json`
- `_reports/SUMMARY.md`

## 验收结果

- 两个 TOC 页面均有对应 Markdown 文件。
- 两个页面均有正确且唯一的 PAGE_ID。
- 两个页面均有配对的 AUTOGEN BEGIN/END 标记。
- 两个 Mermaid 图均通过 Level 0 静态作者规范检查。
- 源码引用均固定到 commit `a8380b01a25ebdb130097b607b3afed2a58d04ba`。
- 没有修改既有 `docs/wiki/` 文件；所有本轮新增路径均在 `docs/wiki/_plugin_smoke_test/`。

## 未执行的真实运行测试

- 未执行原始 Python helper（无本地工作树/执行环境）。
- 未执行 Mermaid.js 浏览器 parse/render，也未执行 Mermaid CLI。
- 未执行原生 Subagent 并行；本次为 sequential fallback。
- 未运行 CMake configure/build/CTest。

因此本次证明了 2.0.2 的上游 phase-spec 依赖解析、TOC/页面生成和静态结构校验链路可完成；不代表 Mermaid 引擎、CMake 构建或 Subagent 并行已通过。
