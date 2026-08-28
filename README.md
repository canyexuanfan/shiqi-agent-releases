# 十七° Agent

十七° Agent 是运行在 Windows 终端里的本地编程智能体：你从哪个项目目录启动，哪个目录就是当前 Workspace。

本仓库仅用于 Windows V1 内测版的安装说明与 Release 下载。

## 安装

在 PowerShell 中执行：

```powershell
$s=& "$env:SystemRoot\System32\curl.exe" -q -fsSL "https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.0-insider.20260828/install.ps1";if($LASTEXITCODE -ne 0){throw 'installer bootstrap download failed'};iex($s|Out-String)
```

> [!IMPORTANT]
> 当前为免费自签名内测版。安装器会先展示发布者和完整证书指纹；只有你明确输入 `INSTALL` 后，Windows 才会请求管理员确认，将公开证书加入 `LocalMachine\TrustedPeople`。证书信任影响本机所有用户。本版本尚无正式 CA、Microsoft Trusted Signing、Microsoft Store 或 SmartScreen 信誉。

本次 Release 的证书指纹：

- SHA-256：`aa9726992ceebe735c91b400f9bef1026f0b4938d21f6019fa2a799601aa8621`
- SHA-1：`FA63626F119339097942FEFE4CA716C448CA1292`

## 运行

```powershell
cd <你的项目目录>
s17
```

- 启动 `s17` 时的当前目录就是本次会话的 Workspace。
- 首次运行会进入 Setup，引导配置数据根、Provider、API Key、模型和 endpoint。
- 常用检查命令：`s17 --version`、`s17 --help`、`s17 doctor`、`s17 --headless`。

## 卸载

```powershell
$s=& "$env:SystemRoot\System32\curl.exe" -q -fsSL "https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.0-insider.20260828/uninstall.ps1";if($LASTEXITCODE -ne 0){throw 'uninstaller bootstrap download failed'};iex($s|Out-String)
```

卸载默认保留用户数据。移除本机证书信任时，Windows 会请求管理员确认。

下载完整性可使用同一 Release 中的 `SHA256SUMS` 核对。问题与建议请提交到 [Issues](https://github.com/canyexuanfan/shiqi-agent-releases/issues)。
