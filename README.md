# 🚀 You-Can-Copy-And-Paste v2.0

<div align="center">

![Version](https://img.shields.io/badge/Version-2.0.0-blue.svg?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows_10%20%7C%2011-lightgrey.svg?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-AutoHotkey_v2-green.svg?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-orange.svg?style=for-the-badge)
![Downloads](https://img.shields.io/github/downloads/你的用户名/你的仓库名/total?style=for-the-badge&color=brightgreen)

**突破在线评测沙箱与严苛编辑器的终极“物理级”输入引擎。**

[English](./README_EN.md) | [简体中文](./README.md)

</div>

---

## 📑 目录 (Table of Contents)
- [📖 项目简介](#-项目简介)
- [🆕 v2.0 重大更新](#-v20-重大更新)
- [✨ 核心特性](#-核心特性)
- [📦 安装与使用](#-安装与使用)
- [⌨️ 快捷键指南](#-快捷键指南)
- [🛠️ 它是如何工作的 (技术原理)](#-它是如何工作的-技术原理)
- [❓ 常见问题 (FAQ)](#-常见问题-faq)
- [⚠️ 免责声明](#-免责声明)

---

## 📖 项目简介

在许多在线代码评测系统（如牛客、LeetCode 严苛模式）、云端企业沙箱或定制的前端编辑器（基于 Monaco / CodeMirror）中，常规的 `Ctrl+V` 或系统剪贴板注入经常会被 JavaScript（如 `onpaste` 事件）无情拦截，或者导致代码格式（缩进、换行）彻底崩坏。

**You-Can-Copy-And-Paste** 的诞生正是为了解决这一痛点。它采用“降维打击”策略：**完全放弃系统级剪贴板粘贴，转而模拟真实人类的物理键盘敲击**。它能将你的代码逐字符、安全地“敲”进任何顽固的输入框中，让你重新夺回复制粘贴的绝对自由。

> **💡 效果演示：**
> *(建议在这里录制一张 GIF 动图：左边是普通 Ctrl+V 报错，右边是使用本工具完美注入代码的过程，并将图片命名为 demo.gif 放在 assets 文件夹下)*
> ![Demo](./assets/demo.gif)

---

## 🆕 v2.0 重大更新

从 v1.0 到 v2.0，我们重写了 100% 的底层逻辑：
* **引擎升级**：摒弃不稳定的旧版剪贴板读写，升级为纯物理级 `SendEvent` 注入。
* **全新 Reverse 特性**：新增反向处理功能，支持文本逆序注入与特殊格式反转，专为绕过顺序行为检测与特殊加密场景设计。
* **现代化 GUI**：新增托盘右键设置面板，配置完全图形化。
* **智能消毒**：内置不可见字符与 `\r` 自动清洗机制。

---

## ✨ 核心特性

- 🛡️ **绝对无视拦截**：将文本转化为底层的键盘扫描码（Scan Code）事件，前端 JS 无法区分这是脚本还是你真的在疯狂敲键盘。
- ⏱️ **仿人类波动延迟 (Human-like Delay)**：内置算法引入正态分布的时间波动。提供 **Fast (极速)**、**Standard (标准)**、**Conservative (保守)** 三种模式，完美伪装人类打字节奏，规避反作弊高频检测。
- 🔄 **Reverse 逆向注入引擎**：支持按行或按字符对剪贴板内容进行逆向解析与注入，应对极其特殊的逆向工程或代码混淆测试。
- 🎨 **智能换行与缩进保护**：注入引擎会在模拟物理回车后自动产生微秒级阻塞（Sleep），给沙箱留出处理“自动缩进（Auto-indent）”的时间，确保代码结构完美。
- 🔌 **纯绿色且防冲突**：支持无感写入注册表实现开机自启。内置修饰键（Ctrl/Shift/Alt）强制释放逻辑，杜绝键盘粘连暴走。

---

## 📦 安装与使用

### 运行环境
- 操作系统：Windows 10 / Windows 11
- 运行依赖：无需安装任何环境，直接运行可执行文件即可。

### 快速启动
1. 访问 [Releases 页面](https://github.com/你的用户名/你的仓库名/releases) 下载最新的 `you-can-copy-and-paste-v2.exe`。
2. 双击运行。如果系统弹出 SmartScreen 拦截，请点击“更多信息” -> “仍要运行”。
3. 查看 Windows 任务栏右下角，出现绿色的 **H** 图标即代表引擎已启动！
4. 右键点击该图标，选择 **Settings** 即可调整输入延迟和自启选项。

---

## ⌨️ 快捷键指南

| 快捷键 | 功能名称 | 详细说明 |
| :--- | :--- | :--- |
| `Ctrl` + `Insert` | **强力捕获** | 清空当前系统剪贴板，安全捕获当前选中的文本并进行格式清洗。 |
| `Shift` + `Insert` | **开始物理注入** | 将捕获的文本转化为物理按键，逐行敲入当前鼠标光标所在的目标窗口。 |
| `Shift` + `Esc` | **紧急熔断** | **极其重要！** 遇到目标窗口卡死或输入失控时，一键强制终止所有注入任务并重置引擎。 |

> 💡 **Tip:** 注入过程中，会在屏幕坐标或鼠标指针处实时显示注入进度（如：`正在注入: 行 45/100`）。

---

## 🛠️ 它是如何工作的 (技术原理)

本工具的核心架构由四大模块协同工作：
1. **Clipboard_Processor (数据清洗层)**：使用 `ClipWait` 确保大型代码块捕获完整。将所有换行符统一规范化为 `\n`，过滤掉可能导致目标编辑器光标乱跳的特殊不可见字符（如 NBSP）。
2. **Delay_Algorithm (时序控制层)**：为每个字符和回车分配动态的 `Sleep` 周期。
3. **Hotkey_Handler (硬件劫持层)**：在捕获到快捷键时，强制发送 `{Ctrl up}{Shift up}{Alt up}`，确保不会因用户按键过快导致后续注入变成无效的组合键。
4. **Injection_Engine (物理注入层)**：调用 Windows 底层 API 的 `SendEvent "{Text}"` 模式。这是确保中文字符和特殊符号原样输出，不触发输入法联想的关键。

---

## ❓ 常见问题 (FAQ)

**Q1: 为什么粘贴中文时，会出现拼音或者乱码？**
> **A:** 因为本工具是在“模拟按键盘”。如果目标窗口开启了中文输入法，工具按下的字母会被输入法截获变成拼音。**解决方案：在按下 `Shift + Insert` 开始注入前，请确保目标窗口处于【英文半角输入状态】。**

**Q2: 注入代码时，格式变成了阶梯状（向右倾斜）怎么办？**
> **A:** 这是因为目标编辑器有很强的“自动缩进”功能。请右键系统托盘，打开 **Settings**，将延迟模式切换为 **Conservative (保守模式)**，给予编辑器足够的渲染时间即可解决。

**Q3: 杀毒软件提示有风险？**
> **A:** 因为本工具涉及注册表读写（开机自启功能）和全局键盘钩子（热键监听），部分杀毒软件可能会误报。本工具完全开源，您可以自行审查 `v2.ahk` 源码并手动编译。

---

## 🤝 参与贡献

我们非常欢迎任何形式的贡献，包括但不限于提交 Bug、增加新功能或优化文档。
1. Fork 本仓库
2. 创建您的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交您的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 将您的更改推送到分支 (`git push origin feature/AmazingFeature`)
5. 发起 Pull Request (PR)

---
 [AutoHotkey v2.0+](https://www.autohotkey.com/)
## ⚠️ 免责声明

本工具仅供学习交流、代码研究及正常办公测试效率提升使用。请严格遵守各在线评测平台（OJ）、考试系统及企业内部网络的安全合规要求。**严禁使用本工具进行任何形式的考试作弊或破坏网络安全的行为。** 因不当使用造成的任何后果，由使用者自行承担，与本工具作者无关。

---
*Developed with ❤️ and AutoHotkey v2.0.*
