# 有意思的 SDR 设备清单（2026-03-11 视角）

这份清单不是“把市面上 SDR 全抄一遍”，而是按实际玩法来挑：

- 真有特色
- 现在仍然活跃、仍能买到
- 和你手里的 `HackRF One` 形成明显互补

## 快速结论

如果只讲“有意思”和“补位价值”，我会把它们分成四类：

1. **便宜耐造的接收机**
2. **高质量接收机**
3. **可收可发的实验平台**
4. **专门干测向/阵列的设备**

---

## 1. 便宜耐造的接收机

### RTL-SDR Blog V4

**有意思在哪**
- 便宜
- 生态大
- 工具多
- 当“专用小工兵”特别合适

**适合干什么**
- ADS-B
- FM / Airband / NOAA / AIS
- `rtl_433`
- 做长期挂台的小接收机

**相对 HackRF 的价值**
- 不是更强，而是更“省心”
- 很多“只接收”的任务，用它比用 HackRF 更像工具而不是实验板

**你为什么会想买**
- 想把 `HackRF` 解放出来做别的
- 想挂一个长期 ADS-B / `rtl_433` / NOAA 小站

**不适合什么**
- 发射
- 高动态范围要求
- 真正严肃的 HF 弱信号

---

## 2. 高质量接收机

### Airspy R2

**有意思在哪**
- 经典的 VHF/UHF 高质量接收机
- 比廉价 RTL 机型更讲究动态范围和接收体验

**适合干什么**
- 广播
- 航空
- VHF/UHF 杂项监听
- 城市复杂环境下的频谱观察

**相对 HackRF 的价值**
- 如果你主要是“收”，它通常比 HackRF 更像一台认真做接收的机器

**不适合什么**
- 发射
- 真正的 HF 主战

### Airspy HF+ Discovery

**有意思在哪**
- 这是很多人拿来认真玩 HF 的“小钢炮”
- 重点不是宽，而是低频段接收质量和抗强信号能力

**适合干什么**
- 短波
- 中波
- 弱信号收听
- 磁环天线玩法

**相对 HackRF 的价值**
- 你如果以后发现自己对 HF / SSB / 短波更有兴趣，它比 HackRF 补位价值大得多

**不适合什么**
- 发射
- 宽带扫很多 GHz 频段

### Airspy Ranger

**有意思在哪**
- 这是 Airspy 较新的高性能宽覆盖接收机路线
- 把 HF+ 系列的“重接收质量”思路，扩到了更宽频段

**适合干什么**
- 一台机器兼顾 HF 到 UHF 的高质量接收
- 想认真做“接收型主力机”

**相对 HackRF 的价值**
- 如果你以后不满足于“能收到”，而是更在乎“收得干净”，这类机器就很有吸引力

### SDRplay RSPdx-R2

**有意思在哪**
- 覆盖 `1 kHz` 到 `2 GHz`
- 三个可切换天线口
- 对 HF/VHF 两头兼顾得比较实际

**适合干什么**
- 从长波、短波一路玩到 VHF/UHF
- 一台机子挂多副天线轮着用

**相对 HackRF 的价值**
- 它不是“实验板”，而是“接收工作台”
- 如果你以后更偏向收听、分析、挂台，它的补位很清楚

**当前官方定价**
- 官方 2024 年发布信息给出的建议零售价是 **$235** 左右，不含税运 [4]

---

## 3. 可收可发的实验平台

### ADALM-PLUTO（PlutoSDR）

**有意思在哪**
- 教学味很浓
- 社区活跃
- 很多人拿它做通信链路实验

**适合干什么**
- 数字通信实验
- GNU Radio
- OFDM / 调制解调练习
- 教学和课程

**相对 HackRF 的价值**
- 它比 HackRF 更偏“通信实验平台”
- 如果你未来想碰协议、链路、基带算法，它很值得看

**不适合什么**
- 宽频段乱扫
- 纯“监听玩具”

### LimeSDR Mini 2.0

**有意思在哪**
- FPGA + 宽带收发
- 开放味更强
- 很多人拿来玩 LTE / 研究型项目 / 自定义波形

**适合干什么**
- 自定义收发链路
- 通信协议实验
- 基带到射频一整套折腾

**相对 HackRF 的价值**
- 它的重点不是“比 HackRF 更好玩”，而是“更偏系统开发”

**现实提醒**
- 官方现货页面显示价格在 **$440** 左右，已经不是“随手买个玩具”的档位 [6]

### bladeRF 2.0 micro

**有意思在哪**
- 2x2 MIMO
- 更像工程设备
- 在蜂窝、研究、协议开发这类场景里很常见

**适合干什么**
- 更严肃的收发实验
- MIMO
- 研究型通信原型

**相对 HackRF 的价值**
- 如果 HackRF 像“宽频瑞士军刀”，bladeRF 更像“工程开发板”

**现实提醒**
- 它通常已经进入明显更贵的级别
- Nuand 官方页面当前可见的 `xA4 THERMAL` 版本价格已在 **$1325** 这个量级 [9]

### USRP B205mini-i

**有意思在哪**
- 这是“正规军”味道很浓的 SDR
- 很多论文、原型系统、工业/科研链路都能看到 USRP 影子

**适合干什么**
- 通信研究
- 课程/实验室
- 更严肃的原型系统开发

**相对 HackRF 的价值**
- 不是拿来随手听台的
- 是为了“我就要认真搭系统”

**不适合什么**
- 纯娱乐监听
- 只想轻松扫台

---

## 4. 专门干测向/阵列的设备

### KrakenSDR

**有意思在哪**
- 五通道相干接收
- 天生就是给测向、被动雷达、阵列玩法准备的

**适合干什么**
- 无线电测向
- 车载 RDF
- 相位阵列实验

**相对 HackRF 的价值**
- 这是和单通道 `HackRF` 完全不同的方向
- 不是“更强的 HackRF”，而是“专门解决 HackRF 不擅长的问题”

**现实提醒**
- 官方现在仍在售，价格是 **$749**，而且还不含天线套件、税费和线材 [5]

---

## 5. 如果按“你这种玩法”来选，最值得看的几台

### 1) `RTL-SDR Blog V4`

最适合当：
- 小工兵
- 长期开机挂任务
- 把 HackRF 从“脏活累活”里解放出来

### 2) `Airspy HF+ Discovery`

最适合当：
- 你未来如果开始对短波、HF、弱信号真正上头

### 3) `SDRplay RSPdx-R2`

最适合当：
- 一台覆盖很宽、又更偏“认真接收”的主力机

### 4) `KrakenSDR`

最适合当：
- 你后面真的决定认真玩无线电测向

### 5) `PlutoSDR`

最适合当：
- 你开始对“通信实验/数字链路”而不是“听信号”更感兴趣

---

## 6. 如果只按“有意思程度”排序

这个排序不是性价比，是“玩法扩展性”：

1. `KrakenSDR`
2. `PlutoSDR`
3. `Airspy HF+ Discovery`
4. `SDRplay RSPdx-R2`
5. `RTL-SDR Blog V4`
6. `bladeRF 2.0 micro`
7. `LimeSDR Mini 2.0`
8. `USRP B205mini-i`

原因很简单：
- `KrakenSDR` 会直接把你带进“阵列/测向”这个新世界
- `PlutoSDR` 会把你带进“通信系统实验”
- `HF+ Discovery` 会把你带进“认真收 HF”

---

## 7. 一句话总结

你已经有了 `HackRF One`，下一台最有补位价值的设备通常不是“另一个差不多的宽带收发机”，而是：

- 要么更偏 **接收质量**：`HF+ Discovery` / `RSPdx-R2`
- 要么更偏 **任务型接收**：`RTL-SDR Blog V4`
- 要么更偏 **阵列/测向**：`KrakenSDR`
- 要么更偏 **通信实验**：`PlutoSDR`

---

## Sources

[1] Airspy `Airspy R2` official product page: https://airspy.com/airspy-r2/  
[2] Airspy `HF+` official page, which explicitly points users to `HF+ Discovery`: https://airspy.com/airspy-hf-plus/  
[3] Airspy `Ranger` official product page: https://airspy.com/airspy-ranger/  
[4] SDRplay `RSPdx-R2` official launch / MSRP page: https://www.sdrplay.com/sdrplay-announces-the-rspdx-r2/  
[5] KrakenRF official `KrakenSDR` product page: https://www.krakenrf.com/product-page/krakensdr  
[6] Crowd Supply `LimeSDR Mini 2.0` product page: https://www.crowdsupply.com/lime-micro/limesdr-mini-2  
[7] Analog Devices official `ADALM-PLUTO` product page: https://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/adalm-pluto.html  
[8] Ettus official `USRP B205mini-i` product page: https://www.ettus.com/all-products/usrp-b205mini-i/  
[9] Nuand official `bladeRF 2.0 micro` product page / store page: https://www.nuand.com/bladerf-1/  
[10] RTL-SDR Blog V4 official user guide: https://www.rtl-sdr.com/V4  

