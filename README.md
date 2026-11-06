# SystemHelper 操作指南

一份尽可能让非技术用户看懂的 Android `SystemHelper` 识别、ADB 用户级卸载与恢复教程。

**这个项目不是一键卸载软件。** `index.html` 是纯静态、可离线打开的操作手册：通过设备分支、逐步指引、真实报错、复制命令、进度勾选以及恢复说明，帮助读者自己确认每一步发生了什么。

## 页面预览

![桌面版指南首页](screenshots/desktop.png)

手机版：[查看图片](screenshots/mobile.png) · 深色模式：[查看图片](screenshots/dark.png)

## 先看页面

直接双击 [`index.html`](index.html)。不需要安装 Node.js、依赖包、网站服务器或 GitHub 账号。页面不上传设备信息，也不会自动执行 ADB 命令。

页面特点：

- 不使用外部 CSS / JavaScript / 字体 / 图片，单 HTML 文件可离线阅读。
- Windows 10 / 11 为主要教程环境；提供基础的 macOS / Linux 终端命令切换。
- 区分 `com.mobiletools.systemhelper` 和 `com.qualcomm.qti.services.systemhelper`。
- 按照“连接 → 核对包名 → 标准操作 → 必要时高级步骤 → 状态验证 → 恢复”的顺序。
- 标准方法被系统拒绝时，不建议其他机型直接照搬特定 Xiaomi 构建的内部接口方法。
- Java 示例源码为单独原创实现；可在页面查看、复制或下载。**该新版示例只通过电脑端 `javac` 编译检查，尚未独立进行真机验证。** 真实成功案例的技术路径详见原作者仓库。

## 实测依据与适用边界

| 项目 | 操作记录 |
|---|---|
| 设备 | Xiaomi 17 Pro Max，16 GB RAM / 1 TB 存储 |
| 构建版本 | HyperOS `OS4.0.6.0.XPBCNXM` |
| 目标包 | `com.mobiletools.systemhelper` |
| 目标应用版本 | `4.0.0-20260910` |
| 普通禁用 | `Cannot disable system packages.` |
| 普通用户级卸载 | `only root can delete system app for a particular user` |
| 最终方法 | Java / DEX 调用 Android 内部包管理接口（使用上游记录中的工具） |
| 最终验证 | User 0 `installed=false`，重启后仍为 `false` |
| 设备基本功能检查 | 移动数据 / 通话 / 短信正常 |

`installed=false` 代表指定用户的安装状态，不等于系统分区中的 APK 已被删除。卸载一个应用也不能证明整部手机没有其他数据收集或网络访问行为。

高级方法只针对**完全相同的系统版本**给出示例，且依赖不受官方保证的内部接口。本文不对其他设备、后续系统升级或恢复结果做兼容性保证。

## 目录结构

```text
systemhelper-guide/
├─ index.html                 # 单文件教程
├─ README.md                  # 本文件
├─ LICENSE                    # 项目原创内容 MIT 许可
├─ CONTRIBUTING.md            # 提交建议与隐私保护
├─ screenshots/               # 项目截图（GitHub README 预览）
└─ tools/
   └─ SystemHelperUserTool.java  # 独立编写的演示源码（未真机复测）
```

## 发布到 GitHub Pages

1. 在 GitHub 创建一个你自己有写入权限的公开仓库，如 `systemhelper-guide`。
2. 把 `index.html`、`README.md`、`LICENSE`、`CONTRIBUTING.md` 和 `tools/` 上传到仓库根目录。
3. 进入仓库 **Settings → Pages → Build and deployment**。
4. Source 选择 **Deploy from a branch**，Branch 选择 `main`，Folder 选择 `/ (root)`，保存。
5. 等待 GitHub 显示公开 Pages 地址；其形式通常为 `https://你的用户名.github.io/systemhelper-guide/`。

如果你希望把网页贡献到 [zd-Ethan/systemhelper](https://github.com/zd-Ethan/systemhelper)，那是别人的仓库。**不能直接上传覆盖其文件**，除非作者给予写入权限。正常合作方式是先提出 Issue、征得对方意见，然后 Fork 仓库、提交新文件并发起 Pull Request；也可以在你自己的仓库独立发布并引用原作者。

## 引用来源及许可

本项目的技术参考与真实成功方法来自：

- [zd-Ethan/systemhelper](https://github.com/zd-Ethan/systemhelper)：小米 14 Pro 与小米 17 Pro Max 免 Root 用户级卸载实测。
- [Google Android Debug Bridge 文档](https://developer.android.com/tools/adb)
- [Google Platform-Tools 下载](https://developer.android.com/tools/releases/platform-tools)
- [Google R8 项目](https://r8.googlesource.com/r8/)

原仓库目前没有明确 LICENSE 文件；**这里不复制、打包或宣称重新许可原作者的 Java 源码**。网站、文案和 `tools/SystemHelperUserTool.java` 为独立制作的项目文件，按本项目 MIT License 许可。Google 的工具与第三方项目各自遵循其许可证，不随本仓库分发二进制文件。

制作 / 前端：**HAPPY Games** · 2026
