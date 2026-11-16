# DeepWiki 2.0.7 — GoogleTest 分支测试报告

## 基本信息
- 插件版本：DeepWiki Codebase Wiki 2.0.7
- 目标仓库：`maxiaoxuxu/googletest`
- 目标分支：`test`
- 源码基准：`277cfa07d637aac85a388d1cb0c6adb585a1432e`
- 输出目录：`docs/wiki/_plugin_v2_0_7_retest/`
- 模式：Automatic workflow 的两页限定范围 smoke-test

## 阶段执行状态

| 阶段 | 状态 | 说明 |
|---|---|---|
| repo-scan | completed with connector fallback | GitHub recursive tree 读取 289 个文件、40 个目录，树未截断；未执行本地 collect_context.py。 |
| toc-design | completed | 生成两页 TOC，源文件映射存在，ID 唯一。 |
| doc-write | completed, sequential fallback | 两页逐页生成；无原生 Subagent 调度。 |
| validate-docs | completed with static checks | PAGE_ID、AUTOGEN、H1、链接、引用路径及 Mermaid Level 0 检查通过；未执行原始 validate_docs_structure.py。 |
| doc-summary | completed | 根据本轮 TOC、页面和静态校验结果生成；未执行原始 generate_summary.py。 |
| incremental-sync | not run | 本轮是新建隔离输出，不是增量更新。 |

## 实际覆盖
- 根 CMake 的 BUILD_GMOCK 分支。
- gtest / gtest_main、gmock / gmock_main 目标及依赖。
- MSVC 与非 MSVC 的 GoogleMock 构建分支。
- gtest-all.cc / gmock-all.cc 聚合编译单元。
- gtest_main.cc / gmock_main.cc 的初始化和 RUN_ALL_TESTS() 入口。

## 校验结果
- 页面 2/2；PAGE_ID 2/2；AUTOGEN 2/2；H1 2/2。
- 页面间链接通过；引用均固定到 `277cfa07d637aac85a388d1cb0c6adb585a1432e`。
- Mermaid 2 个 flowchart，Level 0 静态规则 0 个问题。
- 读取插件提供的 mermaid_lint.py 和测试文件内容，在临时 Python 环境执行回归逻辑：**10/10 tests passed**。覆盖引号 pipe-label 检测与修复、幂等性、middle-label 保留、节点标签保护、非 flowchart 忽略、Markdown fence 范围及 4 条历史回归样例。

10/10 是 Python 静态规则回归测试，不是 Mermaid.js 渲染通过。该规则将 pipe-delimited edge label 的外层包装引号作为插件 authoring style policy，不代表断言 Mermaid parser 必然拒绝这种语法。

## 输出隔离
仅新增本目录下 8 个文件：TOC、2 篇 Markdown、README、context pack、2 份 JSON 校验报告和本 SUMMARY。没有覆盖 docs/wiki 根目录 11 篇既有 Wiki，也没有修改历史测试目录。

## 未执行项与限制
1. 没有目标仓库本地工作树，因此未运行原始 collect_context.py、read_files.py、validate_docs_structure.py、generate_summary.py；使用 GitHub connector 读取和等价静态核验并记录 fallback。
2. Mermaid.js 浏览器 parse/render 与 Mermaid CLI 均为 **not_run**。插件包提供 tools/mermaid/preview.html，可由用户浏览器进行真实解析与 SVG 渲染。
3. 未执行 CMake configure/build/CTest；命令仅为源码支持的复现步骤。
4. 当前宿主没有可观察的原生 Subagent 接口，按页面顺序执行，不能称为并行。
5. 本次是 2 页 smoke-test，不代表对全部 289 个文件逐一完成逐行分析，也不替代完整 11 页 Wiki。

## 结论
**GitHub 分支读取、TOC 设计、两页源码文档生成、固定 commit 引用、隔离输出和 Level 0 静态校验链路完成。** Mermaid.js 真实渲染、CMake 构建及原始本地脚本未执行，不能标记为通过。
