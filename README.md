# HackRF One × SDRangel（Windows 11）笔记

这是一份面向 **Windows 11 + HackRF One + SDRangel** 的个人上手/排障笔记仓库：从“设备能被系统识别”到“成功解码 ADS‑B（1090MHz）”，以及 SDRangel 常见 Channel（通道插件）都能干什么。

## 快速入口

- ADS‑B（飞机 1090MHz）一步到位：`docs/sdrangel-adsb-hackrf-win11.md`
- SDRangel Channel 逐个解释（频段/玩法/大致需要的天线/配件）：`docs/sdrangel-channels-explained.md`
- NOAA APT（137MHz）天气云图：买啥 + 最省事天线：`docs/noaa-apt-antenna-137mhz.md`
- FM 广播扫台（Frequency Scanner）：`docs/sdrangel-fm-scanner-win11.md`
- Frequency Scanner 预置频段解释 + 扫不到原因：`docs/sdrangel-frequency-scanner-presets.md`
- 无线电测向/定位：HackRF 能做什么，为什么 KrakenSDR 更适合：`docs/hackrf-radio-direction-finding.md`
- SDR 设备清单：哪些机器有意思、分别适合干什么：`docs/sdr-devices-overview.md`
- HackRF 发射：在中国合规范围内能做什么：`docs/hackrf-transmit-compliance-cn.md`
- HackRF 桌面闭环通信实验路线图：`docs/hackrf-bench-comm-roadmap.md`

## 最小前置条件（不满足就先别折腾软件）

1) **HackRF 必须先被 Windows 枚举成功**  
   - 设备管理器能看到 `HackRF One (VID_1D50&PID_6089)`（或类似）  
   - HackRF 板子灯通常应至少亮 `3V3 / 1V8 / RF / USB`
2) 若出现“未知 USB 设备(端口重置失败) / Code 43”  
   - 优先排查线缆（很多 micro‑USB 线只有供电或信号质量差）、USB 口、Hub/扩展坞

## 安装位置约定（本机）

为节省 C 盘空间，建议把安装包/软件都放到 E 盘，例如：
- 安装包：`E:\apps\installers\`
- SDRangel：`E:\apps\SDRangel\`

> 仓库只记录“操作与参数”，不强制绑定某个盘符；你可按自己的目录调整。

## 合规提示

请只接收你有权接收、且当地法律允许的无线电信号；涉及业务通信、隐私内容的解码/监听可能违法。
