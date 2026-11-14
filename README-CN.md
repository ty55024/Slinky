<p align="center">
  <img src="assets/ss.png" alt="Open Slinky 横幅" width="350" />
  <br>
  <font size="6"><b>Open Slinky</b></font>
  <br>
  <font size="3">由 Skid Solutions 制作</font>
  <br>
  <font size="2">致谢 cat；
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