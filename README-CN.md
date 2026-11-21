# Slinky
- 感谢 Skid Solutions 团队！

## 如何构建？

### 前置要求

- **LLVM** — `PATH` 中需包含 clang-cl、lld-link、llvm-rc 和 llvm-mt
- **CMake** 3.20 或更高版本
- **Ninja**

### 1. 配置

```powershell
cmake -S . -B build -G Ninja `
  -DCMAKE_TOOLCHAIN_FILE=cmake/toolchain-windows-clang-cl.cmake
```

如果 Ninja 不在 `PATH` 中，请添加
`-DCMAKE_MAKE_PROGRAM=C:/path/to/ninja.exe`。

### 2. 构建

```powershell
cmake --build build
```

### 或使用构建脚本

`build.ps1` 会查找工具链、构建 DLL、构建注入器，并将
`Slinky.exe` 复制到 `dist\`：

---

## 项目结构

```
src/engine/         钩子、JNI/JVMTI、GUI、模块管理器、数学、共享服务
src/logic/          各模块行为（.cpp）及其描述符回调 / 设置页面（.h）
src/platform/       Windows 层、GL 加载器、NanoVG 集成
src/data/           数据表（字体、字符串、描述符）- 链接所必需
include/slinky/     公共头文件
injector/           终端加载器和 DLL 注入器
third_party/        NanoVG 和 GL 头文件
```



## 法律与免责声明

- **隶属关系：** 这是独立开发的项目。它**不是官方的
  SLINKY 产品**，未经原作者批准或与之关联，
  也与 Mojang 或 Zelix Pty Ltd 无关。
- **资源与代码：** `src/data` 中的数据表是客户端自身的数据，为链接所必需；
  所有第三方资源和代码归其各自所有者所有。
- **目的：** 研究与保存。使用风险自负。
