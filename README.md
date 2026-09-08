# 十七° Agent

十七° Agent 是运行在 Windows 终端里的本地编程智能体：你从哪个项目目录启动，哪个目录就是当前 Workspace。

本仓库仅用于 Windows V1 内测版的安装说明与 Release 下载。

## 安装

在 PowerShell 中执行：

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.8-insider.20260908/install.ps1' | iex
```

第一项交互是“请选择语言 / Choose your language”，可用方向键选择简体中文或 English。随后可修改程序安装位置；程序、CLI 和更新暂存都保存在所选位置。安装阶段不会询问 Workspace。

> [!IMPORTANT]
> 当前为免费自签名内测版。首次安装会显示简短的证书信任说明以及“继续安装 / 取消”选择；选择继续后，Windows 会显示一次管理员确认，将公开证书加入 `LocalMachine\TrustedPeople`。证书信任影响本机所有用户。本版本尚无正式 CA、Microsoft Trusted Signing、Microsoft Store 或 SmartScreen 信誉。

本次 Release 的证书指纹：

- SHA-256：`4f184d4a24699cda4cfbe1a7db0f3bd6ca484e4c1bf6c4353be51e8c2ba523c1`
- SHA-1：`AEF9DCD4258EF5454442BCEDAF3E21F18543F5C0`

## 运行

```powershell
cd <你的项目目录>
s17
```

- 启动 `s17` 时的当前目录就是本次会话的 Workspace。
- 首次运行会进入 Setup，引导配置数据根、Provider、API Key、模型和 endpoint；数据根默认建议 `ProgramRoot\data`，可修改。
- Windows 系统盘只保留系统要求的小型位置指针、凭据库记录、证书信任和注册元数据；模型、运行时、下载、更新暂存和用户数据不会静默回落到 C 盘。
- 常用检查命令：`s17 --version`、`s17 --help`、`s17 doctor`、`s17 --headless`。

## 卸载

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.8-insider.20260908/uninstall.ps1' | iex
```

卸载默认保留用户数据。移除本机证书信任时，Windows 会请求管理员确认。

下载完整性可使用同一 Release 中的 `SHA256SUMS` 核对。问题与建议请提交到 [Issues](https://github.com/canyexuanfan/shiqi-agent-releases/issues)。
