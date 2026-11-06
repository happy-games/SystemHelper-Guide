[English](./README.md) | [简体中文](./README.zh-CN.md)

# SystemHelper Guide

An ADB guide for identifying SystemHelper on Android, checking its install state, and deciding whether to disable it, remove it for User 0, or restore it. It starts with the USB connection. You run each command yourself.

**[Open the online guide](https://happy-games.github.io/SystemHelper-Guide/)**

> **Check the full package name.** This guide covers `com.mobiletools.systemhelper`. Leave `com.qualcomm.qti.services.systemhelper`, a separate Qualcomm system component, alone.

## Why some users remove SystemHelper

Public analyses link the preinstalled component on some mainland China Android phones to China Unicom device management. November 2026 reports on specific samples identified fields such as IMEI, IMSI, ICCID, app lists, usage time, data usage, and network or location information. The reports identified logic for sending data to `dm.wo.com.cn:18080`. One report also analyzed network traffic from its test phone.

App lists and usage records can reveal more when tied to device or SIM identifiers. Some owners disable or remove the package for their user to limit further collection by this component. The reports do not establish that it is malware, that every phone behaves the same way, or that every field reaches the server. Removing it cannot undo past transfers or establish what other services collect.

## Supported devices and test record

The read-only ADB checks can be used on other Android phones with USB debugging. Standard disable and uninstall commands depend on the manufacturer and system build. The advanced result below applies only to the recorded phone and build.

| Item | Recorded result |
| --- | --- |
| Device | Xiaomi 17 Pro Max, 16 GB RAM / 1 TB |
| System | HyperOS `OS4.0.6.0.XPBCNXM` |
| Target | `com.mobiletools.systemhelper`, version `4.0.0-20260910` |
| Root and bootloader | Root access not used. Bootloader not unlocked. |
| Standard commands | Disable and user-level uninstall were both refused. |
| Advanced method | The upstream tool called the internal package manager interface as ADB shell. User 0 still showed `installed=false` after reboot. |
| Basic checks | Mobile data, calls, and SMS worked. |

The test used the upstream tool. The website’s separate Java example passed desktop compilation only.

## Disclaimer, risks, and recovery

This guide is for technical research and personal device management. Use it only on a device you own or are authorized to manage. You decide whether to make changes and assume the risks of doing so. Compatibility, continued device functionality, and recovery depend on the device and system build.

Removal is optional. This component may support carrier registration or device management. Back up important data and record the original package state before changing it. User-level removal changes the install state for User 0 and leaves the original system APK in place. If that APK is still available, the guide shows how to try recovery with `install-existing` and verify the result. Recovery depends on the build and was not tested in the recorded case.

## How to use the guide

Open the online guide above. Start with the read-only checks and follow the sections for standard ADB, verification, and recovery. Choose **简体中文** in the header to read the Chinese version. The guide keeps the commands and test output identical in both languages.

## Sources and license

- [zd-Ethan — upstream user-level removal procedure and test record](https://github.com/zd-Ethan/systemhelper)
- [acxun — primary HyperOS device-management analysis](https://github.com/acxun/hyperos-dm-report)
- [DreamingCats — primary analysis of a realme sample](https://github.com/DreamingCats/com.mobiletools.systemhelper_analysis)
- [Bufanche — coverage of SystemHelper reporting](https://bufanche.com/guides/unicom-systemhelper/)
- [Android Debug Bridge documentation](https://developer.android.com/tools/adb)

HAPPY Games publishes the guide and its independent example under the [MIT License](./LICENSE). Upstream code and third-party tools follow their own terms. See the [contribution guide](./CONTRIBUTING.md) for reporting another device.
