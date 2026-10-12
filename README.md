<a id="top"></a>

<div align="center">

# MediaCreationTool.bat

**Windows 安装介质工具 · Windows installation media tool**

![Windows 11 26H2](https://img.shields.io/badge/Windows_11-26H2-0078D4?style=flat-square)
![Architecture x64](https://img.shields.io/badge/26H2-x64-555555?style=flat-square)
[![License MIT](https://img.shields.io/badge/License-MIT-2EA44F?style=flat-square)](LICENSE)

[简体中文](#chinese) · [English](#english) · [下载 ZIP / Download ZIP](https://github.com/a317634186/MediaCreationTool.bat/archive/refs/heads/main.zip)

</div>

---

<a id="chinese"></a>

## 简体中文

下载 Windows 镜像、创建 ISO 或 USB 安装盘的 Media Creation Tool 包装脚本。本分支新增 **Windows 11 26H2（x64）**，保留原有 Windows 10/11 选项，工具和镜像均从微软服务器获取。

脚本提供 TPM 2.0 等安装检查的绕过处理，供 **Intel 老款 Mac** 等设备尝试安装 Windows 11。当前本分支最新选项为 **26H2**。

> [!IMPORTANT]
> **26H2 + Intel Mac 尚未进行实机安装验证。** 绕过检查不等于保证兼容；本项目不是微软或 Apple 官方支持方案。

### 快速开始

1. [下载 ZIP](https://github.com/a317634186/MediaCreationTool.bat/archive/refs/heads/main.zip)，完整解压后运行 `MediaCreationTool.bat`。
2. 选择 **11_26H2**（默认版本）。
3. 需要原版安装介质时选择 **MCT Defaults**，按提示选择语言和版本。
4. 选择 **ISO 文件**保存镜像，或选择 **USB 闪存驱动器**制作安装盘。

需要简体中文时，取消“对这台电脑使用推荐的选项”，再选择中文（简体）。**制作 USB 安装盘会清除所选 U 盘的数据。**

命令行预选版本：

```bat
MediaCreationTool.bat 11_26H2
```

`26H2`、`2610` 是同一版本的别名。26H2 下载路径建议在 **Windows 10/11 + Windows PowerShell 5.1** 下使用，仅支持 **x64**。脚本不能直接在 macOS 中运行。

### 选择合适的预设

| 预设 | 用途 | 安装介质修改 |
| :--- | :--- | :--- |
| **MCT Defaults** | 通过微软工具创建原版安装介质 | 不加入脚本的绕过处理或附加文件 |
| **Select** | 手动选择版本、语言和可用架构，再指定目标 | 默认加入脚本处理 |
| **Auto ISO** | 按检测到的配置创建 ISO | 默认加入脚本处理 |
| **Auto USB** | 按检测到的配置制作安装 U 盘，仍需手动选盘 | 默认加入脚本处理 |
| **Auto Upgrade** | 按检测到的配置直接启动升级 | 使用脚本辅助升级流程 |

在名称或参数中加入 `def` 可禁用介质修改。自动化预设继承自原项目，尚未针对 26H2 完成安装验证。

### Intel 老款 Mac 与 TPM 2.0

面向 **Intel x64 Mac** 上的 Windows 安装尝试，**不适用于 Apple Silicon（M 系列）**。本项目安装的是 Windows，不是 macOS。

1. 在 Mac 已有的 Windows 环境中运行脚本，或使用另一台 Windows 电脑准备介质。
2. 选择 **11_26H2 → Auto ISO / Auto USB / Select**，尝试生成包含安装检查绕过处理的介质。
3. **不要选择 MCT Defaults，也不要加入 `def`**，否则不会加入这些介质修改。
4. 安装前备份数据，并准备对应机型的 Boot Camp Windows 支持软件（驱动）；分区和启动方式需按具体机型确认。

绕过 TPM 2.0 检查不能补齐 CPU 缺失的指令，也不能解决驱动和固件兼容问题。上述流程尚未在 **26H2 + Intel Mac** 上实机验证，不能保证所有老款 Mac 安装成功。

Apple 的 [Boot Camp 官方指南](https://support.apple.com/en-gb/102622) 针对 Intel Mac 上的 Windows 10；Windows 11 官方仍要求 [TPM 2.0 等硬件条件](https://learn.microsoft.com/en-gb/windows/whats-new/windows-11-requirements)。

### 可选版本

| 系统 | 菜单选项 |
| :--- | :--- |
| Windows 10 | 1507 · 1511 · 1607 · 1703 · 1709 · 1803 · 1809 · 1903 · 1909 · 20H1 · 20H2 · 21H1 · 21H2 · 22H2 |
| Windows 11 | 11_21H2 · 11_22H2 · 11_23H2 · **11_26H2** |

24H2、25H2、26H1 尚未加入。旧版本保留原下载逻辑，链接可用性取决于微软服务器。

### 26H2 更新与验证

**2026-10-12 更新：**

- 新增版本菜单、命令行别名和正确的 26H2 版本显示。
- 通过微软接口动态获取 `products.cab`，校验大小和 SHA256，支持目录格式 2.1。
- 校验 x64 镜像属于 **26300 / 26H2**；返回其他版本时停止处理。
- 校验微软工具的数字签名，保留镜像 SHA256 和官方许可协议链接。
- 修复提权后的版本选择恢复，并为版本菜单增加滚动。

| 验证项 | 当前状态 |
| :--- | :--- |
| 微软镜像目录 | 2026-10-12 核对为 **26300.9457**，包含简体中文消费版及企业版条目 |
| 下载与完整性 | 目录下载、大小、SHA256、微软工具签名通过；简体中文消费版镜像链接可访问 |
| 脚本流程 | 菜单、版本参数、提权选择恢复、目录转换与打包、错误目录与错误版本拒绝处理通过 |
| 完整 ISO、USB 制作、安装、升级 | **尚未完成验证** |
| Intel Mac 实机兼容性 | **尚未验证** |

具体可选版本以微软工具和目录为准。微软接口若切换到其他版本或改变目录格式，需要更新脚本。

### 高级部署与项目来源

原脚本支持通过名称或参数传入版本、语言、架构、版本类型和 `no_update` 等选项；自动化预设可生成 `auto.cmd`、`PID.txt`、`EI.cfg` 和安装应答文件，并将 `$ISO$` 内容加入介质。不同预设和配置会影响实际修改内容。

完整的原始预设说明、部署示例及历史日志保存在 [原项目文档（英文存档）](docs/README.upstream.md)。其中的旧版本说明不代表当前验证范围。

本项目基于 [AveYo/MediaCreationTool.bat](https://github.com/AveYo/MediaCreationTool.bat)，采用 [MIT 许可证](LICENSE)。微软官方安装资源：[下载 Windows 11](https://www.microsoft.com/zh-cn/software-download/windows11)。

[切换到 English](#english) · [返回顶部](#top)

---

<a id="english"></a>

## English

A Media Creation Tool wrapper for downloading Windows images and creating ISO files or USB installation media. This fork adds **Windows 11 26H2 (x64)** while retaining the existing Windows 10/11 options. Tools and images are downloaded from Microsoft servers.

The script includes workarounds for TPM 2.0 and other setup checks, allowing users of **older Intel Macs** and other devices to attempt a Windows 11 installation. **26H2** is the newest option in this fork.

> [!IMPORTANT]
> **Installation of 26H2 on physical Intel Mac hardware has not been validated.** Bypassing checks does not guarantee compatibility. This project is not an officially supported Microsoft or Apple solution.

### Quick start

1. [Download the ZIP](https://github.com/a317634186/MediaCreationTool.bat/archive/refs/heads/main.zip), extract it completely, and run `MediaCreationTool.bat`.
2. Select **11_26H2**, the default version.
3. For media without the script's setup modifications, choose **MCT Defaults**, then select your language and edition.
4. Choose **ISO file** to save an image, or **USB flash drive** to create installation media.

To select Simplified Chinese, clear “Use the recommended options for this PC” and choose Chinese (Simplified). **Creating USB installation media erases the selected USB drive.**

Preselect the version from the command line:

```bat
MediaCreationTool.bat 11_26H2
```

`26H2` and `2610` are aliases for the same version. For the 26H2 download path, **Windows 10/11 with Windows PowerShell 5.1** is recommended. This path supports **x64 only**. The script cannot run directly in macOS.

### Choose a preset

| Preset | Purpose | Setup modifications |
| :--- | :--- | :--- |
| **MCT Defaults** | Create original installation media using Microsoft's tool | No script bypass changes or additional files |
| **Select** | Choose the edition, language, available architecture, and destination | Script modifications enabled by default |
| **Auto ISO** | Create an ISO using detected settings | Script modifications enabled by default |
| **Auto USB** | Create USB media using detected settings; drive selection remains manual | Script modifications enabled by default |
| **Auto Upgrade** | Start an upgrade using detected settings | Uses the script-assisted upgrade workflow |

Adding `def` to the filename or arguments disables media modifications. Automation presets are inherited from the original project and have not undergone complete installation testing on 26H2.

### Older Intel Macs and TPM 2.0

This workflow is for attempting a Windows installation on an **Intel x64 Mac**. It **does not support Apple Silicon (M-series)**. The operating system being installed is Windows, not macOS.

1. Run the script in an existing Windows installation on the Mac, or prepare the media on another Windows PC.
2. Select **11_26H2 → Auto ISO / Auto USB / Select** to attempt to create media with the script's setup-check workarounds.
3. **Do not select MCT Defaults or add `def`**, as these disable the media modifications.
4. Back up your data and prepare the Boot Camp Windows support software (drivers) for your model. Confirm the appropriate partition layout and boot method for that Mac.

Bypassing TPM 2.0 checks cannot add missing CPU instructions or fix driver and firmware compatibility. This workflow has not been tested on physical **Intel Mac hardware with 26H2**, so successful installation on every older Mac cannot be guaranteed.

Apple's [official Boot Camp guide](https://support.apple.com/en-gb/102622) covers Windows 10 on Intel Macs. Windows 11 still officially requires [TPM 2.0 and other hardware capabilities](https://learn.microsoft.com/en-gb/windows/whats-new/windows-11-requirements).

### Available versions

| Operating system | Menu options |
| :--- | :--- |
| Windows 10 | 1507 · 1511 · 1607 · 1703 · 1709 · 1803 · 1809 · 1903 · 1909 · 20H1 · 20H2 · 21H1 · 21H2 · 22H2 |
| Windows 11 | 11_21H2 · 11_22H2 · 11_23H2 · **11_26H2** |

24H2, 25H2, and 26H1 have not been added. Older versions retain their original download logic; link availability depends on Microsoft servers.

### 26H2 changes and validation

**Updated 2026-10-12:**

- Added the version menu entry, command-line aliases, and correct 26H2 labels.
- Retrieve `products.cab` dynamically from Microsoft's API, verify its size and SHA256, and support catalog format 2.1.
- Verify that x64 media belongs to **26300 / 26H2**; stop if the API returns another version.
- Verify Microsoft's tool signature and preserve media SHA256 values and official license links.
- Restore version selections after elevation and add scrolling to the version menu.

| Check | Current status |
| :--- | :--- |
| Microsoft media catalog | Verified as **26300.9457** on 2026-10-12, including Simplified Chinese consumer and business entries |
| Downloads and integrity | Catalog download, size, SHA256, and Microsoft tool signature passed; the Simplified Chinese consumer image URL was reachable |
| Script workflow | Menu, version arguments, selection after elevation, catalog conversion and repacking, and rejection of corrupt or incorrect-version catalogs passed |
| Complete ISO download, USB creation, installation, and upgrade | **Not yet validated** |
| Physical Intel Mac compatibility | **Not yet validated** |

Available editions depend on Microsoft's tool and catalog. The script needs updating if Microsoft's API switches to another release or changes the catalog format.

### Advanced deployment and credits

The original script accepts version, language, architecture, edition, and options such as `no_update` through its filename or arguments. Automation presets can generate `auto.cmd`, `PID.txt`, `EI.cfg`, and setup answer files, and add `$ISO$` content to the media. Actual modifications depend on the selected preset and configuration.

The complete original preset descriptions, deployment examples, and historical changelog are preserved in the [original project documentation](docs/README.upstream.md). Historical version claims do not describe the current validation scope.

Based on [AveYo/MediaCreationTool.bat](https://github.com/AveYo/MediaCreationTool.bat), under the [MIT license](LICENSE). Official Microsoft installation resources: [Download Windows 11](https://www.microsoft.com/en-us/software-download/windows11).

[切换到简体中文](#chinese) · [Back to top](#top)
