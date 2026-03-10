# Agent Notes (HackRF One × SDRangel on Windows 11)

本仓库是柠檬叔的个人笔记：围绕 **HackRF One + SDRangel（Windows 11）** 做 ADS‑B、NOAA APT 等接收实验，并记录参数/排障与“频道插件”说明。

## Quick Commands（PowerShell）

- 检查 HackRF 是否被系统识别（应看到 `HackRF One` + `VID_1D50&PID_6089`）：
  - `Get-PnpDevice -PresentOnly | Where-Object { $_.InstanceId -match 'VID_1D50&PID_6089' } | Format-Table -AutoSize Status,Class,FriendlyName,InstanceId`
- 查看 HackRF 驱动/服务（常见为 `WinUSB`）：
  - `$id=(Get-PnpDevice -PresentOnly | Where-Object { $_.InstanceId -match 'VID_1D50&PID_6089' } | Select-Object -First 1 -ExpandProperty InstanceId); Get-PnpDeviceProperty -InstanceId $id -KeyName DEVPKEY_Device_Service`
- 典型“线不行/枚举失败”症状（端口重置失败 / Code 43）：
  - `Get-PnpDevice -PresentOnly | Where-Object { $_.FriendlyName -match '端口重置失败|Unknown USB Device|RESET_FAILURE' } | Format-Table -AutoSize Status,Problem,Class,FriendlyName,InstanceId`

## Repo Map

- ADS‑B（1090MHz）一步到位：`docs/sdrangel-adsb-hackrf-win11.md`
- SDRangel Channel 逐个解释：`docs/sdrangel-channels-explained.md`
- NOAA APT（137MHz）天线与采购清单：`docs/noaa-apt-antenna-137mhz.md`

## Hardware Notes（柠檬叔当前这块板子的“已知事实”）

### HackRF One

- 设备：HackRF One（USB 枚举正常时：`USB\\VID_1D50&PID_6089\\...`）
- USB 线：micro‑USB **必须是数据线且质量要好**；线材问题常见症状是设备管理器出现“未知 USB 设备(端口重置失败)”/`USB\\RESET_FAILURE`/Code 43
- 指示灯：枚举正常时通常可看到 `3V3 / 1V8 / RF / USB` 亮

### 射频/时钟接口（不要插错）

- **天线接 `ANT`**（板子丝印 `ANT` 的 SMA 口，收/发都走这个口）
- `CLK IN` 不是天线口：它是外部参考时钟输入（通常 10MHz），不用就盖防尘帽

### 板载/插板时钟模块

- 当前板子上已安装一个 **`10.000MHz` 时钟模块**（插在板子上那种模块）
- 作用：提升频率稳定度/准确度；对 ADS‑B/NOAA APT 通常“没有也能玩”，但对更窄带/更严格的场景更有帮助

## Environment Notes

- OS：Windows 11；默认用 PowerShell（命令用 `;` 串联，不用 `&&`）
- 磁盘：尽量把安装包/软件装在 **E 盘**（C 盘空间紧张）

## Safety

- HackRF **可发射**：默认只做接收；任何发射/功放/上天线的操作必须先征得用户明确同意，并遵守当地法律法规与安全规范。

