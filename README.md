# 十七° Agent

十七° Agent 是终端中的通用智能体。本仓库只提供安装说明与二进制发行资产，不发布产品源码。

## Windows 安装与更新

当前内测版：[v0.0.18-insider.20260926](https://github.com/canyexuanfan/shiqi-agent-releases/releases/tag/v0.0.18-insider.20260926)。

已有受管安装可直接原位更新，无需先卸载；程序位置、数据位置和配置会保留。打开普通、非管理员 Windows PowerShell，任选以下同一安装器的入口。

推荐入口（Windows 自带 curl，最多三次完整下载尝试）：

```powershell
$s17Bootstrap=$null;$s17BootstrapOk=$false;foreach($s17Attempt in 1..3){try{$s17Bootstrap=& "$env:SystemRoot\System32\curl.exe" -q -fsSL --proto '=https' --proto-redir '=https' --max-redirs 5 --connect-timeout 10 --max-time 25 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v0.0.18-insider.20260926/install.ps1' 2>$null}catch{$s17Bootstrap=$null};if($LASTEXITCODE -eq 0 -and $s17Bootstrap){$s17BootstrapOk=$true;break};$s17Bootstrap=$null;if($s17Attempt -lt 3){Start-Sleep -Seconds 2}};if(-not $s17BootstrapOk){throw 'installer bootstrap download failed'};iex($s17Bootstrap|Out-String)
```

简短兼容入口（PowerShell 网络功能正常的账户）：

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v0.0.18-insider.20260926/install.ps1' | iex
```

先选简体中文或 English。全新安装可以选择程序位置；已有安装进入原位更新或修复。普通安装、更新、恢复和卸载为当前用户级操作，不导入机器证书、不安装 MSIX，也不主动请求 UAC。

当前为免费自签名内测发行，非商业 CA 或 SmartScreen 信誉保证。不需要关闭系统安全功能；安装器仍严格验证发行身份、完整性和安装后命令可用性。

## 首次配置与使用

安装成功后关闭安装窗口，打开新的普通 PowerShell，进入自己的安全测试目录：

```powershell
Get-Command s17
s17 --help
s17 doctor
s17
```

裸 `s17` 在当前终端进入自己的 TUI。首次或未完成配置在同一界面内选择 Quick / Custom / Blank、数据位置、服务商、凭据与模型；方向键选择、Enter 确认，凭据以 `*` 掩码显示。支持连续浏览与搜索服务商和模型，优先动态模型目录，再使用数据根缓存和内置兜底。配置完成后进入自然语言 Agent。

从哪个目录启动 `s17`，哪个目录就是当前 Workspace。程序安装位置、数据存储位置和 Workspace 是三个不同概念。数据根可以放到非 C 盘；系统盘仅保留系统要求的小型指针、凭据库和注册元数据，可控大数据不会静默回落到 C 盘。

文件写入与进程操作需要逐次确认；拒绝不应产生操作效果。真实服务商、输入法、读屏及终端体验仍需用户独立验收，自动测试不代替真人体验。

## 卸载与保留数据重装

在普通 PowerShell 中执行：

```powershell
$s17Bootstrap=$null;$s17BootstrapOk=$false;foreach($s17Attempt in 1..3){try{$s17Bootstrap=& "$env:SystemRoot\System32\curl.exe" -q -fsSL --proto '=https' --proto-redir '=https' --max-redirs 5 --connect-timeout 10 --max-time 25 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v0.0.18-insider.20260926/uninstall.ps1' 2>$null}catch{$s17Bootstrap=$null};if($LASTEXITCODE -eq 0 -and $s17Bootstrap){$s17BootstrapOk=$true;break};$s17Bootstrap=$null;if($s17Attempt -lt 3){Start-Sleep -Seconds 2}};if(-not $s17BootstrapOk){throw 'uninstaller bootstrap download failed'};iex($s17Bootstrap|Out-String)
```

默认保留数据，只移除受管程序与精确 PATH 条目，不删除未知用户文件。重新安装回原位置可继续使用保留的数据。

故障反馈请说明步骤、实际结果与预期，勿上传 Key。可提交到 [Issues](https://github.com/canyexuanfan/shiqi-agent-releases/issues)。
