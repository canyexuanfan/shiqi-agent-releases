# 十七° Agent

十七° Agent 是运行在 Windows 终端里的本地编程智能体：你从哪个项目目录启动，哪个目录就是当前 Workspace。

本仓库仅用于 Windows V1 内测版的安装说明与 Release 下载。

## 安装

在 PowerShell 中执行：

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.10-insider.20260913/install.ps1' | iex
```

第一项交互是“请选择语言 / Choose your language”，可用方向键选择简体中文或 English。随后可修改程序安装位置；程序、CLI 和更新暂存都保存在所选位置。安装阶段不会询问 Workspace。

> [!IMPORTANT]
> 当前为免费自签名内测版，尚无正式 CA、Microsoft Trusted Signing、Microsoft Store 或 SmartScreen 信誉，Windows、浏览器或安全软件仍可能显示下载或未知发布者提示。安装器会在后台校验固定清单、文件哈希、签名及公开证书身份；普通安装、更新和卸载均为当前用户级操作，不导入系统证书，也不会主动请求管理员权限或弹出 UAC。

本次 Release 的证书指纹：

- SHA-256：`85aea21c384caceb4d09157da13188874497aa153a2716714070cf4e29dbb17c`
- SHA-1：`E4C94E0835A1C4AE37324037E839A593D3D0EA7C`

v1.0.10 改为完整的用户级零 UAC 安装链，并保留 Windows PowerShell 5.1 下公网下载的有界重试、断点
恢复和失败关闭。它同时补齐可修改 Program Root 与 Data Root、失败后继续 Setup、配置后更新、保留数据
重装以及安装后真实 Agent 文件与进程操作；下载后的完整文件仍须通过 `SHA256SUMS` 和发行清单校验。

## 运行

```powershell
cd <你的项目目录>
s17
```

- 启动 `s17` 时的当前目录就是本次会话的 Workspace。
- 首次运行会进入 Setup，引导配置数据根、Provider、API Key、模型和 endpoint；数据根默认建议 `ProgramRoot\data`，可修改。
- Windows 系统盘只保留系统要求的小型位置指针、凭据库记录和注册元数据；模型、运行时、下载、更新暂存和用户数据不会静默回落到 C 盘。
- 常用检查命令：`s17 --version`、`s17 --help`、`s17 doctor`、`s17 --headless`。

## 卸载

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.10-insider.20260913/uninstall.ps1' | iex
```

卸载默认保留用户数据，并且不会主动请求管理员权限或弹出 UAC。

下载完整性可使用同一 Release 中的 `SHA256SUMS` 核对。问题与建议请提交到 [Issues](https://github.com/canyexuanfan/shiqi-agent-releases/issues)。
