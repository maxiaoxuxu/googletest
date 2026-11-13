# DeepWiki 插件运行时冒烟测试

- 目标仓库：`maxiaoxuxu/googletest`
- 源码基准：`main @ a8380b01a25ebdb130097b607b3afed2a58d04ba`
- 写入分支：`test`
- 输出范围：仅 `docs/wiki/_plugin_smoke_test/`
- 页面：`01_build_graph.md`、`02_aggregate_units.md`
- 执行方式：GitHub Connector 读取源码；页面任务按独立页面顺序执行（当前没有可观察的原生 Subagent 并行调度能力）。
- 说明：这是插件 2.0.2 修复后的独立冒烟测试输出，不覆盖原有 `docs/wiki/` 文件。
