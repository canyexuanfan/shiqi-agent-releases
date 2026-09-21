# 十七° Agent

十七° Agent 是 CLI-first 的通用智能体。你从哪个目录启动 `s17`，哪个绝对目录就是本次 Workspace。

本仓库只提供 Windows V1 内测版的安装说明与二进制发行资产，不发布产品源码。

## 安装

当前内测版为 [v1.0.17-insider.20260921](https://github.com/canyexuanfan/shiqi-agent-releases/releases/tag/v1.0.17-insider.20260921)。

打开普通、非管理员 Windows PowerShell，复制这一整行：

```powershell
$s17Bootstrap=$null;$s17BootstrapOk=$false;foreach($s17Attempt in 1..3){try{$s17Bootstrap=& "$env:SystemRoot\System32\curl.exe" -q -fsSL --proto '=https' --proto-redir '=https' --max-redirs 5 --connect-timeout 10 --max-time 25 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.17-insider.20260921/install.ps1' 2>$null}catch{$s17Bootstrap=$null};if($LASTEXITCODE -eq 0 -and $s17Bootstrap){$s17BootstrapOk=$true;break};$s17Bootstrap=$null;if($s17Attempt -lt 3){Start-Sleep -Seconds 2}};if(-not $s17BootstrapOk){throw 'installer bootstrap download failed'};iex($s17Bootstrap|Out-String)
```

PowerShell 网络功能正常时，也可以使用简短兼容入口；两条命令执行的是同一个安装器：

```powershell
irm 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.17-insider.20260921/install.ps1' | iex
```

先选简体中文或 English，再选择程序安装位置。严格识别的旧中断安装可以恢复；已有安装进入原位修复，陌生非空目录不会被覆盖。普通安装、更新、恢复和卸载均为当前用户级操作，不导入机器证书、不安装 MSIX，也不会主动弹 UAC。

这是免费自签名内测版，尚无商业 CA 或 SmartScreen 信誉；浏览器或安全软件可能显示未知发布者提示。不需要关闭系统安全功能，安装器仍会严格验证发行身份、完整性和安装后可用性。

## 配置与实际使用

安装成功后关闭安装窗口，打开新的普通 PowerShell，进入自己的安全测试目录：

```powershell
Get-Command s17
s17 --help
s17 doctor
s17
```

首次裸 `s17` 进入同语言 Setup，配置就绪后直接进入 Agent。自行选择 Quick/Custom/Blank、数据位置、Provider、凭据、模型与 endpoint；凭据输入隐藏，请勿上传 Key。

程序位置、数据位置和当前 Workspace 是三件不同的事。数据根默认建议 `ProgramRoot\data`，可以另外放到非 C 盘。C 盘仅保留系统要求的小型位置指针、凭据库记录和注册元数据；模型、下载、更新暂存和可控数据不会静默回落到 C 盘。

输入普通自然语言任务即可使用。文件写入与进程操作需要逐次确认；拒绝后不应产生效果。换目录启动会改变 Workspace，但保留已保存的配置和数据根。真实 Provider、输入法与终端体验请自行完整测试；自动验收不能代替真人体验。

## 更新、卸载与保留数据重装

再次执行安装命令即可原位更新或修复；数据根、语言和配置应保持，不重复 PATH。

需要卸载时，在普通 PowerShell 执行：

```powershell
$s17Bootstrap=$null;$s17BootstrapOk=$false;foreach($s17Attempt in 1..3){try{$s17Bootstrap=& "$env:SystemRoot\System32\curl.exe" -q -fsSL --proto '=https' --proto-redir '=https' --max-redirs 5 --connect-timeout 10 --max-time 25 'https://github.com/canyexuanfan/shiqi-agent-releases/releases/download/v1.0.17-insider.20260921/uninstall.ps1' 2>$null}catch{$s17Bootstrap=$null};if($LASTEXITCODE -eq 0 -and $s17Bootstrap){$s17BootstrapOk=$true;break};$s17Bootstrap=$null;if($s17Attempt -lt 3){Start-Sleep -Seconds 2}};if(-not $s17BootstrapOk){throw 'uninstaller bootstrap download failed'};iex($s17Bootstrap|Out-String)
```

卸载默认保留数据，只移除当前用户受管程序与精确 PATH 条目；未知用户文件不会被删除。重新安装回原位置后，可以继续使用保留的数据和配置。

失败时保留不含凭据的提示和诊断日志位置，不手工删安装目录、写 PATH 或导入证书。反馈请说明步骤、实际结果与预期，可提交到 [Issues](https://github.com/canyexuanfan/shiqi-agent-releases/issues)。
