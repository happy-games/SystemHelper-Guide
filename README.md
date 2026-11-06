# SystemHelper 操作指南

用 ADB 查清 Android 手机上的 SystemHelper 是哪个应用，再决定是否禁用、为主用户卸载或恢复。教程从连接手机讲起，适合第一次使用 ADB 的读者。每条命令都由你在电脑上确认执行，网页不会操作手机。

**[打开中文操作指南](https://happy-games.github.io/systemhelper-guide/)**

> **先核对包名。** 本教程处理的是 `com.mobiletools.systemhelper`。名字相近的高通组件 `com.qualcomm.qti.services.systemhelper` 请保留。

## 从哪里开始

| 你现在要做什么 | 从这里读 |
| --- | --- |
| 第一次用 ADB，想先把手机连上 | [快速开始](https://happy-games.github.io/systemhelper-guide/#step1) |
| 看到 SystemHelper，想确认手机上是哪一个包 | [识别与检查](https://happy-games.github.io/systemhelper-guide/#step3) |
| 在对应的小米 17 Pro Max 构建上遇到权限拒绝 | [高级方案与适用条件](https://happy-games.github.io/systemhelper-guide/#step6) |
| 已经操作，想复查结果或恢复 | [验证](https://happy-games.github.io/systemhelper-guide/#step7) · [恢复](https://happy-games.github.io/systemhelper-guide/#step8) |

网页提供深浅主题和可复制命令。通用流程以 Windows 为主，也可以在其他 Android 手机上参考连接、识别和状态检查。能否禁用或卸载取决于设备和系统版本。

## 小米 17 Pro Max 实测摘要

| 项目 | 记录 |
| --- | --- |
| 设备 | Xiaomi 17 Pro Max，16 GB RAM / 1 TB |
| 系统 | HyperOS `OS4.0.6.0.XPBCNXM` |
| 目标应用版本 | `4.0.0-20260910` |
| 标准 ADB 流程 | 禁用和用户级卸载均被系统拒绝 |
| 高级方案 | 使用上游临时工具调用内部包管理接口，重启后 User 0 仍为 `installed=false` |

这里的 `installed=false` 表示主用户的安装登记已取消。系统分区中的原始 APK 仍在。高级方案的成功记录限于上表的设备和构建，网页自带的独立 Java 示例仅通过电脑端编译检查。

操作前请备份重要资料。其他设备若被系统拒绝，先回读安装状态。系统更新后可以再查一次，恢复是否可用也取决于设备。

## 离线阅读与仓库文件

下载仓库 ZIP 并解压，双击 [`index.html`](./index.html) 即可在浏览器阅读。网页无需安装 Node.js 或运行构建。要连接手机，再下载 [Android Platform-Tools](https://developer.android.com/tools/releases/platform-tools)。

| 文件 | 用途 |
| --- | --- |
| [`index.html`](./index.html) | GitHub Pages 教程首页，样式和脚本内联 |
| [`README.md`](./README.md) | 当前仓库首页说明 |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | 机型记录、问题反馈和脱敏要求 |
| [`LICENSE`](./LICENSE) | 本项目的 MIT 许可 |

## 来源与许可

高级方案的原始思路、工具和公开验证记录来自 [zd-Ethan/systemhelper](https://github.com/zd-Ethan/systemhelper)。ADB 命令的用法见 [Android 官方文档](https://developer.android.com/tools/adb)。

教程编排、页面及独立编写的示例由 HAPPY Games 整理，采用 [MIT 许可](./LICENSE)。上游源码和第三方工具各自遵循其发布条款。
