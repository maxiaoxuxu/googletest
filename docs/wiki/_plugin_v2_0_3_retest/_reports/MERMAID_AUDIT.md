# Mermaid 全量静态审计（GoogleTest Wiki）

## 范围与方法

- 分支：`test`
- 审计对象：`docs/wiki/` 根目录 11 篇原始 Wiki、`_plugin_smoke_test/` 2 篇冒烟测试、`_plugin_v2_0_3_retest/` 2 篇复测页。
- 实际提取 Mermaid fenced blocks：9 个。
- 检查内容：围栏配对、图类型声明、节点标签、边标签写法；并将插件的 Mermaid 规则与 Mermaid 官方 Flowchart 语法文档对照。
- 本次没有 Mermaid.js 浏览器执行环境，也没有安装 Mermaid CLI（`mmdc`）；因此本报告是静态审计，不冒充 9/9 的运行时 parse/render 通过。

## 发现

| 文件 | Mermaid 块 | 发现 | 处置/状态 |
|---|---:|---|---|
| `docs/wiki/08_expectations.md` | 1 | 使用 `C -->|"no"| D`、`C -->|"yes"| E`。属于插件规范所推荐、但不应作为 pipe-label 的带引号形式 | 标记为待修复；原始 Wiki 未覆盖 |
| `docs/wiki/_plugin_v2_0_3_retest/08_expectations.md` | 1 | 使用 `D -->| "No" | E`、`D -->| "Yes" | F`；GitHub 页面截图已实际显示 Parse error on line 5 | 已在复测副本改为 `D -->|No| E` / `D -->|Yes| F` |
| 其余 7 个块 | 7 | 未发现本次定位的 quoted pipe-edge-label 模式 | 仅静态通过；未声称 Mermaid.js 运行时通过 |

## 根因

插件仓库 `.apm/skills/wiki/references/mermaid_policy.md` 的 “Edge Labels” 示例将 `A -->|"Yes"| B` 写成正确用法；语言示例也沿用该模式。生成器按这条规则写图，导致图本身携带不兼容/错误的边标签语法。

同一插件的静态审计说明只检查有限的作者规范，并非完整 Mermaid parser。此前复测报告把两个图标记为 Level 0 无错误，但该检查没有拦截 quoted pipe edge labels，造成 false negative。

## 修正规则

- 普通 pipe edge label 使用无引号文本：`A -->|Yes| B`。
- 如边标签必须包含特殊字符或需要完整 quoted label，使用 Mermaid 文档支持的中置标签形式，例如 `A -- "edge label" --> B`，并以目标 Mermaid 版本实测为准。
- 不要把节点标签的双引号规则机械套用到 pipe-delimited edge label。

参考：Mermaid 官方 Flowchart 语法  
https://mermaid.js.org/syntax/flowchart.html

## 插件层应修复的内容（本次未修改插件仓库）

1. 修订 `.apm/skills/wiki/references/mermaid_policy.md`：删除所有 `-->|"label"|` 的“正确示例”，替换为无引号 pipe label；对需要引号的边标签使用中置标签形式。
2. 在静态校验中增加规则：检测 `-->|"… "|` / `-->| "…" |` 这类 quoted pipe edge label，至少给出错误而不是静默通过。
3. Phase 4 必须运行 Mermaid.js `parse()` + `render()` 或 `mmdc`；若运行环境不可用，应将状态报告为 `not_run/unverified`，不能写成 `invalid_blocks: []` 并暗示通过。
4. 每次修复后重新扫描全部 Markdown Mermaid blocks，而不是只复查报错页面。

## 当前结论

- 已修正本轮复测副本中的截图报错写法。
- 原始 `docs/wiki/08_expectations.md` 仍保留原状，避免覆盖用户原文；它存在同类风险。
- 其余 7 个图仅完成静态模式审计。
- Mermaid.js / Mermaid CLI 的最终渲染验证仍未执行；需在可联网的浏览器打开插件 `preview.html` 后，将修正后的 9 个图逐一粘贴/导入验证，或在本地安装并运行 `mmdc`。
