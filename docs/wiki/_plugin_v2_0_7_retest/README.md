# DeepWiki 2.0.7 — GoogleTest 分支重新测试

- 目标仓库：`maxiaoxuxu/googletest`
- 目标分支：`test`
- 源码基准：`277cfa07d637aac85a388d1cb0c6adb585a1432e`
- 输出目录：`docs/wiki/_plugin_v2_0_7_retest/`
- 范围：2 页隔离 smoke-test，覆盖 CMake 构建图、聚合编译单元和 main 入口。

## 页面
1. [CMake 构建入口与目标依赖](01_build_graph.md)
2. [聚合编译单元与测试入口](02_aggregate_units.md)

## 记录
- [TOC](toc.yaml)
- [上下文包](_context/context_pack.json)
- [结构校验](_reports/structure_validation.json)
- [Mermaid 静态检查](_reports/mermaid_invalid.json)
- [执行报告](_reports/SUMMARY.md)

本轮不覆盖 `docs/wiki/` 根目录已有 Wiki，也不修改历史 smoke-test、2.0.3 或 2.0.4 测试目录。
