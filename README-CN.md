<p align="center">
  <img src="assets/ss.png" alt="Open Slinky 横幅" width="350" />
  <br>
  <font size="6"><b>Open Slinky</b></font>
  <br>
  <font size="3">由 Skid Solutions 制作</font>
  <br>
  <font size="2">致谢 cat；</font>
</p>

---

<p align="center">
  <a href="https://discord.gg/AEwatvnvSf">https://discord.gg/AEwatvnvSf</a>
</p>

<p align="center">
  <img src="assets/jak.jpg" alt="Java 挂钩" height="150" />
  <img src="assets/hack.jpg" alt="卸载" height="150" />
  <img src="assets/deobf2.png" alt="符号恢复" height="150" />
  <img src="assets/deobf.jpg" alt="可读名称" height="150" />
</p>

---

## 关于

Open Slinky 是适用于 Minecraft 1.8.9 的 Slinky 客户端的 C++ 实现。
该客户端以原生 DLL 形式注入游戏进程；它通过 JVMTI 在 Java 字节码层面挂钩游戏，
将事件分发给模块系统，并通过 NanoVG 渲染其界面。

---

## 如何构建

### 前置要求

- **LLVM** — `PATH` 中需包含 clang-cl、lld-link、llvm-rc 和 llvm-mt
- **CMake** 3.20 或更高版本
- **Ninja**
- **Windows x64**
- **Java Development Kit 8** — Minecraft 1.8.9 的运行时；编译 DLL 时不需要

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

输出：

- `build/slinky.dll`

### 或使用构建脚本

`build.ps1` 会查找工具链、构建 DLL、构建注入器，并将
`Slinky.exe` 复制到 `dist\`：

```powershell
.\build.ps1                 # 客户端 + 注入器
.\build.ps1 -Clean          # 先清空 build\
.\build.ps1 -Client         # 仅 DLL
.\build.ps1 -Injector       # 仅注入器（使用现有 DLL）
.\build.ps1 -Jobs 8         # 限制并行度
```

`build.bat` 可在资源管理器中执行相同操作。

脚本首先在 `PATH` 中查找工具，然后在其常见安装位置
（`C:\Program Files\LLVM\bin`、`C:\Program Files\CMake\bin`、
`C:\Strawberry\c\bin` 等）中查找。注入器需要 MinGW-w64 `g++`。

### 运行

使用 `LoadLibrary` 将 `slinky.dll` 注入正在运行的 Minecraft 1.8.9 进程。
启动在独立线程上运行；客户端界面通过其 GUI 键打开。关闭最后一个界面标签页
会卸载客户端：它会保存设置、移除 Java 挂钩并释放该库。

`injector/` 中的注入器会打包该库并为你完成此操作：

```powershell
Slinky.exe            # 查找 Minecraft 并注入
Slinky.exe --list     # 列出 Java 进程
Slinky.exe --help     # 所有选项
```

---

## 项目结构

```txt
src/engine/         挂钩、JNI/JVMTI、GUI、模块管理器、数学、共享服务
src/logic/          各模块行为（.cpp）及其描述符回调 / 设置页面（.h）
src/platform/       Windows 层、GL 加载器、NanoVG 集成
src/data/           数据表（字体、字符串、描述符）— 链接所必需
include/slinky/     公共头文件
injector/           终端加载器和 DLL 注入器
third_party/        NanoVG 和 GL 头文件
```

## 说明

- 设置和配置文件存储在 `~/.slinky`（`settings`、`profiles/`）中。
- `src/data/*.s` 和 `src/platform/win/chkstk.s` 是数据和编译器支持段，
  不是客户端代码。

## 致谢

- 原始客户端：Slinky

## 法律与免责声明

- **隶属关系：** 这是一个独立开发项目。它**不是官方 SLINKY 产品**，
  未经原始作者批准或与其关联，也与 Mojang 或 Zelix Pty Ltd 无关。
- **资产与代码：** `src/data` 表是客户端自身链接所需的数据；
  所有第三方资产和代码归其各自所有者所有。
- **用途：** 研究与保存。使用风险自负。
