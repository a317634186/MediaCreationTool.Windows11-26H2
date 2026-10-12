# MediaCreationTool.bat — Windows 11 26H2

用于下载 Windows 安装镜像和创建安装介质的 Media Creation Tool 包装脚本。本分支新增 **Windows 11 26H2（x64）**，保留原有 Windows 10 和 Windows 11 版本选项。工具和镜像均从微软服务器获取。

提供 TPM 2.0 等安装检查的绕过功能，供 **Intel 芯片的老款苹果 Mac** 等设备尝试安装 Windows 11。当前本分支最新选项为 **26H2**；尚未完成 Intel Mac 实机兼容性验证，不能保证所有机型安装成功。

## 快速使用

1. 点击仓库 **Code → Download ZIP**，完整解压后运行 `MediaCreationTool.bat`。
2. 在版本菜单选择 **11_26H2**（默认选项）。
3. 需要原版安装介质时选择 **MCT Defaults**，按微软工具提示选择语言和版本；Intel 老款 Mac 需要尝试绕过检查时，参阅下方说明。
4. 选择 **ISO 文件**保存镜像，或者选择 **USB 闪存驱动器**制作安装盘。

需要简体中文时，在微软工具中取消“对这台电脑使用推荐的选项”，再选择中文（简体）。制作 USB 安装盘会清除所选 U 盘的数据。

也可以在命令行预选版本，再在弹出的菜单选择预设：

```bat
MediaCreationTool.bat 11_26H2
```

`26H2` 和 `2610` 是同一版本的别名。使用 26H2 下载路径建议在 Windows 10/11 上运行，并使用 Windows PowerShell 5.1；本脚本的 26H2 路径支持 x64，不支持 x86 或 ARM64。

## Intel 老款 Mac：尝试绕过 TPM 2.0 检查

适用于使用 **Intel x64 处理器**、准备安装 Windows 的老款 Mac。这里的系统是 Windows 11，不是 macOS；**不适用于 Apple Silicon（M1、M2、M3、M4 等）**。正确名称为 **TPM 2.0**。

1. 在 Mac 已有的 Windows 环境中运行脚本，或者使用另一台 Windows 电脑准备安装介质；`.bat` 不能直接在 macOS 中运行。
2. 选择 **11_26H2**，再选择 **Auto ISO**、**Auto USB** 或 **Select**，尝试生成包含脚本安装检查绕过处理的介质。
3. **不要选择 MCT Defaults，也不要在脚本名称或参数中加入 `def`**，这两种方式会禁用脚本的安装介质修改。
4. 安装前备份数据，并准备对应 Mac 机型的 Boot Camp Windows 支持软件（驱动）。分区和启动方式需要根据具体机型确认。

绕过 TPM 2.0 检查不会补齐 CPU 缺失的指令、修复驱动或解决固件兼容问题。脚本现有绕过方法在 **26H2 + Intel Mac** 上尚未进行实机验证；这些步骤描述的是可尝试的流程，不是已验证的机型支持承诺。

Apple 的 [Boot Camp 官方安装指南](https://support.apple.com/en-gb/102622) 针对 Intel Mac 上的 Windows 10。Windows 11 官方仍要求 [TPM 2.0 等硬件条件](https://learn.microsoft.com/en-gb/windows/whats-new/windows-11-requirements)，本节属于非官方安装尝试方案。

## 版本列表

| 系统 | 菜单选项 |
| --- | --- |
| Windows 10 | 1507、1511、1607、1703、1709、1803、1809、1903、1909、20H1、20H2、21H1、21H2、22H2 |
| Windows 11 | 11_21H2、11_22H2、11_23H2、**11_26H2** |

24H2、25H2 和 26H1 尚未加入本脚本。旧版本保留原下载逻辑，其链接可用性取决于微软服务器。

## 26H2 更新说明（2026-10-12）

- 新增 `11_26H2` 菜单项、命令行别名和正确的版本显示。
- 通过微软更新元数据接口动态获取 `products.cab`，校验文件大小及 SHA256，适配目录格式 2.1。
- 校验目录中的 x64 镜像确实属于 **26300 / 26H2**；接口返回其他版本时停止，避免误下载。
- 下载并校验微软 Media Creation Tool 的数字签名，保留镜像 SHA256 和微软原有许可协议链接。
- 修复 Windows 11 版本选择在提权重启后的恢复，并为版本菜单增加滚动。

2026-10-12 核对的微软镜像目录版本为 **26300.9457**，包含简体中文消费版（家庭版／专业版等）及企业版条目。具体可选版本以微软工具和目录为准。

已验证官方目录下载、目录哈希、工具签名、菜单选择、版本参数、提权选择恢复、目录转换和重新打包，以及错误目录和版本不符时的拒绝处理。简体中文消费版镜像链接已通过 HTTP 可用性检查。

**尚未完成完整 ISO 下载、系统安装、升级或 USB 制作验证。** 原脚本的 Auto Upgrade、自动制盘和绕过硬件检查功能未针对 26H2 做完整安装验证；需要原版安装介质时，推荐使用 **MCT Defaults**。微软目录将来切换到其他版本或改变格式时，需要更新脚本。

官方安装资源：[下载 Windows 11](https://www.microsoft.com/zh-cn/software-download/windows11)。本项目是第三方脚本，并非微软官方工具本身；原始项目来自 [AveYo/MediaCreationTool.bat](https://github.com/AveYo/MediaCreationTool.bat)，遵循仓库中的 [MIT 许可证](LICENSE)。

## Original presets and deployment documentation

The original preset documentation below describes the inherited automation features. This fork adds Windows 11 26H2 x64 catalog support; full installation and upgrade testing for those automation features has not been completed on 26H2. Use **MCT Defaults** for media without the script's setup modifications.

The screenshot shows an earlier version of the menu:

<img src="preview.png" alt="Earlier MediaCreationTool.bat version menu">

Presets  
-------  
1 ***Auto Upgrade*** with detected media, script assists setupprep for upgrading directly  
> _- can keep files and apps on more scenarios where os and target edition does not match_  
> _- can switch detected edition by adding EditionID to script name_  
> _- can troubleshoot upgrade failing by adding `no_update` to script name_  
> _- auto defaults to 11, so pass version as well for 10: `auto 21H2 MediaCreationTool.bat`_  

2 ***Auto ISO*** with detected media in current folder directly _(or C:\ESD if run from zip)_  
> _- can override detected media by adding edition name / language / arch to script name_  
> _- example: `21H1 Education en-US x86 iso MediaCreationTool.bat`_  

3 ***Auto USB*** with detected media in specified usb target  
> _- for data safety, this is not fully automated - must select the usb drive manually in GUI_  

4 ***Select*** with user picked Edition, Language, Arch (x86,x64,both) - on specified target  
> _- implicit choice, includes setup override files (disable by adding `def` to script name)_  

5 ***MCT Defaults*** runs unassisted, creating media without script modification  
> _- no added files, script passes `products.xml` to MCT and quits without touching media_  

1-4 presets will modify created media in the following ways:  
> _- write `auto.cmd` to run on demand for auto upgrade with edition switch and skip tpm_  
> _- write `$ISO$` folder content (if it exists) at the root of the media_  
> _if you previously used $OEM$ content, must now place it in `$ISO$\sources\$OEM$\`_  
> _- write `sources\PID.txt` to preselect edition at media boot or within windows (if configured)_  
> _- write `sources\EI.cfg` to prevent product key prompt on Windows 11 consumer media (11 only)_  
> _- write `AutoUnattend.xml` in boot.wim to enable local account on Windows 11 Home (11 only)_  
> _- patch `winsetup.dll` in boot.wim to remove windows 11 setup checks when booting from media (11 only)_  
> _- can disable by adding `def` to script name for a default, untouched MCT media_  

Simple deployment  
-----------------   
**auto.cmd** is behind ***Auto Upgrade*** preset via GUI  
Can run it fully unnatended by renaming script with `auto MediaCreationTool.bat`  
Makes it easy to upgrade keeping files and apps when the OS edition does not match the media  
Should allow upgrade from Ultimate, PosReady, Embedded, LTSC or Enterprise Eval as well  

Generated script is added to the created media so you can run it again at any time  
It is fairly generic - it will detect available editions in install.esd, pick a suitable index,  
then set EditionID in the registry to match; can even force another edition, keeping files and apps!  
On 11, it will try to skip setup checks (can disable this behavior with script var)  
Finally, it sets recommended setup options with least amount of issues on upgrades  

> Let's say the current OS is Enterprise LTSC 2019, and you use the business media to upgrade:  
> **auto.cmd** selects Enterprise index and adjust EditionID to Enterprise in the registry (backed up as EditionID_undo)  
> Maybe you also want to switch edition,  
> ex. by renaming the script to  `ProfessionalWorkstation MediaCreationTool.bat`:  
> **auto.cmd** selects Professional index and sets EditionID to ProfessionalWorkstation in the registry.  
>   
> Let's say the OS is Windows 7 Ultimate or PosReady, and you use the consumer media to upgrade:  
> **auto.cmd** selects Professional index, and sets EditionID to Professional or Enterprise, respectively.  
> In all cases, the script tries to pick an existing index, else a compatible one to keep files and apps on upgrade.  
>   
> Let's say you have a dozen PCs spread with versions: 7, 8.1, 10 and editions: Ultimate, Home, Enterprise LTSB..  
> If you need to upgrade all to the latest 10 version and only use Pro, you could rename the script as:  
> `auto 21H2 Pro MediaCreationTool.bat`  
>
> Can even add a VL / MAK / retail product key in the same way to take care of licensing differences.  
> The script also picks up any `$ISO$` folder in the current location - for $OEM$ branding, configuration, tweaks etc.  

Changelog  
---------  
_No need to right-click Run as Admin, script will ask itself. Directly saving the Raw files no longer breaks line endings_  
_We did it! We broke [the previous gist](https://git.io/MediaCreationTool.bat)_ ;) So this is the new home. **Thank you all!**  

[discuss on MDL](https://forums.mydigitallife.net/threads/universal-mediacreationtool-wrapper-script-create-windows-11-media-with-automatic-bypass.84168/)  

```
2026.10.12: Windows 11 26H2 x64 (26300) support in this fork
            dynamic Microsoft catalog API, SHA256/size and Microsoft MCT signature verification, catalog format 2.1
            reject non-26H2 catalogs; preserve official EULA links; scroll version menu; restore elevated selection

2018.10.10: reinstated 1809 [RS5]! using native xml patching for products.xml; fixed syntax bug with exit/b
2018.10.12: added data loss warning for RS5
2018.11.13: RS5 is officially back! + greatly improved choices dialog - feel free to use the small snippet in your own scripts
2019.05.22: 1903 [19H1]
2019.07.11: 1903 __release_svc_refresh__ and enable DynamicUpdate by default to grab latest CU
2019.09.29: UPDATED 19H1 build 18362.356 ; RS5 build 17763.379 and show build number
            added LATEST MCT choice to dinamically download the current version (all others have hard-coded links)
2019.11.16: 19H2 18363.418 as default choice (updated hard-coded links)
2020.02.29: 19H2 18363.592
2020.05.28: 2004 19041.264 first release
2020.10.29: 20H2 and aniversary script refactoring to support all MCT versions from 1507 to 20H2!!!
2020.10.30: hotfix utf-8, enterprise on 1909+
2020.11.01: fix remove unsupported options in older versions code breaking when path has spaces.. pff
2020.11.14: generate latest links for 1909,2004; all xml editing now in one go; resolved known cannot run script issues
2020.11.15: one-time clear of cached MCT, as script generates proper 1.0 catalog for 1507,1511,1703 since last update
            fixed compatibility with naked windows 7 powershell 2.0 / IPv6 / optional import $OEM$ / 1803+ business typo
            updated executables links for 1903 and 2004
2020.11.17: parse first commandline parameter as version, example: MediaCreationTool.bat 1909
2020.12.01: attempt to fix reported issues with 1703; no other changes (skipping 19042.630 leaked esd because it is broken)
2020.12.11: 20H2 19042.631; fixed pesky 1703 decryption bug on dual x86 + x64; improved cleanup; label includes version
2021.03.20: pre-release 21H1; optional auto upgrade or create media presets importing $OEM$ folder and key as PID.txt
2021.05.23: 21H1 release; enhanced script name args parsing, upgrade from embedded, auto.cmd / PID.txt / $OEM$ import
2021.06.06: create iso directly; enhanced dialogs; args from script name or commandline; refactoring is complete!
2021.08.04: done fiddling
2021.09.03: 21H2, both 10 and 11 [unreleased]
2021.09.25: Windows 11
            with Skip TPM Check on media boot as well as on dynamic update (standalone toggle script available)
            final touches for improved script reliability; enhanced auto upgrade preset; win 7 powershell 2.0 compatible
2021.09.30: fix Auto Setup preset not launching.. automatically
2021.10.04: fix for long standing tr localization quirks; Skip TPM Check v2 (ifeo-based instead of wmi)
2021.10.05: 11 22000.194 Release (rofl W11 MCT has limited capabilities, so still using 21H1 MCT because it works fine)
2021.10.09: outstanding refactoring around Windows 11 MCT; minimize while waiting MCT; unified 7 - 11 appearence
2021.10.20: create generic iso if no edition arg; use Downloads folder; no 11 setup checks on boot in VirtualBox; fixes #2
2021.10.23: 11 22000.258
            more intuitive presets; 11 setup override via AutoUnattend.xml or via boot.wim (for VirtualBox 5.x) with FIX arg
            only reliable ui automation; enhanced script output
2021.11.03: multiple download methods; improved automation; improved auto.cmd; moved autounattend.xml to boot.wim
            revising 11 setup bypass (wip) - not being content with any methods is the reason why I've not updated in a while
2021.11.09: skip windows 11 upgrade checks with setup.exe (not just auto.cmd); no server label; local account on 11 home
            auto.cmd has more fixes to keep files and apps on upgrade; reliable ui automation; alternative downloaders 
2021.11.15: 11 22000.318
            write output to script folder (or C:\ESD if run from zip); style: more consistent separation of arguments
            20H2 builds with esd size above 4GB that had to be reverted at 19042.631: en,de,es,pt,fr,it,jp,zh (MCT limits)
2021.11.16: 10 19044.1288 - official release of 10 21H2
            10 19043.1348 - newest 10 build - don't ask why ms is releasing these as such, it's not the first time
2021.12.07: skip windows 11 upgrade checks only via auto.cmd - just ignore server label, please
2021.12.15: fix regression with 1507-1709 not getting the correct fallback esd; fix dev '-noe' not autoclosing script
2021.12.22: improved auto.cmd handling of mismatched OS and target edition, obey 'def', 'auto' upgrades 7 to 10, not 11
2022.03.16: prevent launch errors when run from non-canonical paths; USBLayout progress; pickup $ISO$ dir to add on media
            DU in 11: auto installs 22000.556 atm; older skip_11_checks, without Server label; Home offline local account
2022.03.18: fix regression with Auto Upgrade; removed powershell -nop arg (issue #41); enhanced 11 AutoUnattend.xml
2022.03.20: stable - all issues ironed out; improved script ui; upgrade keeping files from Eval editions too
            last squash I promise ;)
```
