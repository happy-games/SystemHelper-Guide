[English](./README.md) | [简体中文](./README.zh-CN.md)

# SystemHelper 操作指南

用 ADB 识别 Android 手机上的 SystemHelper，查看安装状态，再决定是否禁用、为 User 0 卸载或恢复。教程从连接手机讲起，每条命令都由你自己执行。

**[打开在线操作指南](https://happy-games.github.io/SystemHelper-Guide/)**

> **先核对完整包名。** 本教程处理 `com.mobiletools.systemhelper`。名称相似的 `com.qualcomm.qti.services.systemhelper` 是独立的高通系统组件，请保留。

## 为什么有人选择卸载 SystemHelper？

公开分析将部分中国大陆版 Android 手机预装的该组件与中国联通终端设备管理联系起来。2026 年 11 月公开的样本分析报告提到了 IMEI、IMSI、ICCID、应用列表、使用时长、流量及网络或位置字段。研究者也发现了向 `dm.wo.com.cn:18080` 发送数据的逻辑，其中一份报告分析了测试手机的实际网络流量。

应用列表和使用记录与设备或 SIM 标识关联后，可能透露更多使用习惯。有些用户选择禁用或为当前用户卸载，以减少该组件继续采集数据的可能性。现有报告并未证实它是恶意软件，也不能说明每台手机行为相同，或每项数据都已送达。卸载无法撤回此前可能上传的数据，也不能说明其他服务收集了什么。

## 适用设备与实测记录

支持 USB 调试的其他 Android 手机也可以参考只读检查。标准禁用和卸载能否执行取决于厂商和系统构建。以下高级方案的结果只适用于实测设备和构建。

| 项目 | 实测结果 |
| --- | --- |
| 设备 | Xiaomi 17 Pro Max，16 GB RAM / 1 TB |
| 系统 | HyperOS `OS4.0.6.0.XPBCNXM` |
| 目标 | `com.mobiletools.systemhelper`，版本 `4.0.0-20260910` |
| Root 与 Bootloader | 未使用 Root，未解锁 Bootloader。 |
| 标准命令 | 禁用和用户级卸载均被系统拒绝。 |
| 高级方案 | 上游工具以 ADB shell 身份调用内部包管理接口，重启后 User 0 仍显示 `installed=false`。 |
| 基础功能 | 移动数据、电话和短信正常。 |

真机实测使用的是上游工具。网页中的独立 Java 示例仅通过电脑端编译检查。

## 免责声明、风险与恢复

本指南仅供技术研究和个人设备管理参考。请仅在自己拥有或有权管理的设备上操作。是否修改由你自行决定，相关风险由你承担。方法能否适用、设备功能是否受影响，以及能否恢复，都取决于机型和系统构建。

是否卸载由你决定。该组件可能承担运营商注册或设备管理功能。修改前请备份重要资料并记录目标包原有状态。用户级卸载只改变 User 0 的安装状态，原始系统 APK 仍保留。若 APK 仍可用，教程说明如何尝试用 `install-existing` 恢复并验证结果。能否恢复取决于系统构建，本次实测未执行恢复。

## 如何使用教程

打开上面的在线指南，先做只读检查，再按需查看标准 ADB 操作、验证和恢复。网页默认显示英文，点击顶部的 **简体中文** 即可切换。两种语言中的命令和实测输出完全一致。

## 来源与许可

- [zd-Ethan — 用户级卸载原始方案与实测记录](https://github.com/zd-Ethan/systemhelper)
- [acxun — HyperOS 终端管理组件原始分析](https://github.com/acxun/hyperos-dm-report)
- [DreamingCats — realme 样本原始分析](https://github.com/DreamingCats/com.mobiletools.systemhelper_analysis)
- [不翻车 — SystemHelper 数据上报相关报道](https://bufanche.com/guides/unicom-systemhelper/)
- [Android Debug Bridge 官方文档](https://developer.android.com/tools/adb)

教程与独立示例由 HAPPY Games 整理，采用 [MIT 许可](./LICENSE)。上游代码和第三方工具各自遵循其发布条款。提交其他机型记录前，请阅读[贡献说明](./CONTRIBUTING.zh-CN.md)。
