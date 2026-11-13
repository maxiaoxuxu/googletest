<!-- PAGE_ID: googletest_11_build_testing -->

<details>
<summary>相关源码文件</summary>

本页引用以下源码与项目文档：

- ([README.md:11-32](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/README.md#L11-L32))
- ([CMakeLists.txt:1-35](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/CMakeLists.txt#L1-L35))
- ([CMakeLists.txt:18-24](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L18-L24))
- ([CMakeLists.txt:110-156](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L110-L156))
- ([CMakeLists.txt:11-18](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L11-L18))
- ([CMakeLists.txt:68-118](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L68-L118))
- ([CMakeLists.txt:166-225](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L166-L225))
- ([CMakeLists.txt:120-215](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L120-L215))
- ([gtest_main.cc:53-65](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest_main.cc#L53-L65))

</details>

# 构建与项目自测

> **相关页面**：[项目总览与模块边界](./01_project_overview.md) · [参数化、Typed、Death 与动态测试](./06_test_variants.md)

---

<!-- BEGIN:AUTOGEN googletest_11_build_testing_main -->
## 构建与项目自测

## 版本与语言标准

仓库当前源码树的根 CMake 设置版本为 1.18.0；README 明确要求 1.18.x 使用 C++17。([README.md:11-17](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/README.md#L11-L17)) ([CMakeLists.txt:1-35](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/CMakeLists.txt#L1-L35))

## 构建目标

根 CMake 默认开启 GoogleMock；GTest CMake 提供 `gtest` / `gtest_main`，GMock CMake 提供 `gmock` / `gmock_main`。([CMakeLists.txt:19-35](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/CMakeLists.txt#L19-L35)) ([CMakeLists.txt:110-156](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L110-L156)) ([CMakeLists.txt:68-118](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L68-L118))

## 编译框架自身的测试

GTest 和 GMock 自身的测试默认不构建，需分别开启 `gtest_build_tests` 和 `gmock_build_tests`。GTest 项目包含 death-test、environment、listener、parameterized-test、repeat、skip 等测试；GMock 项目包含 actions、cardinalities、function-mocker、matchers、spec-builders 等测试。([CMakeLists.txt:18-24](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L18-L24)) ([CMakeLists.txt:166-225](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L166-L225)) ([CMakeLists.txt:11-18](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L11-L18)) ([CMakeLists.txt:120-215](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L120-L215))

一个可供本地验证的 CMake 流程是：

~~~bash
cmake -S . -B build \
  -Dgtest_build_tests=ON \
  -Dgmock_build_tests=ON
cmake --build build
ctest --test-dir build --output-on-failure
~~~

这是基于仓库 CMake 选项设计的运行建议，不是本次已经执行的测试结果。本次只检查了 CMake 配置和测试目标声明，没有在目标环境实际编译或运行 CTest。

**Sources**：([README.md:11-32](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/README.md#L11-L32))、([CMakeLists.txt:1-35](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/CMakeLists.txt#L1-L35))、([CMakeLists.txt:18-24](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L18-L24))、([CMakeLists.txt:110-156](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L110-L156))、([CMakeLists.txt:11-18](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L11-L18))、([CMakeLists.txt:68-118](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L68-L118))、([CMakeLists.txt:166-225](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/CMakeLists.txt#L166-L225))、([CMakeLists.txt:120-215](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googlemock/CMakeLists.txt#L120-L215))、([gtest_main.cc:53-65](https://github.com/maxiaoxuxu/googletest/blob/a8380b01a25ebdb130097b607b3afed2a58d04ba/googletest/src/gtest_main.cc#L53-L65))
<!-- END:AUTOGEN googletest_11_build_testing_main -->

---
