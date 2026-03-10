# SDRangel「Channel」列表逐个解释（面向 HackRF/Win11）

这份文档解释你截图里那一长串 **Channel（接收通道插件）** 都是干嘛的、能玩什么、一般要什么频段/天线/配件；并穿插一些“用 HackRF 能不能胜任”的现实建议。

> 重要概念：**Channel ≠ 硬件设备**  
> - **硬件/输入设备（Device / Sample Source）**：HackRF/RTL-SDR/文件输入…决定“我能收到哪段频谱、带宽多大”。  
> - **Channel（通道插件）**：在设备提供的宽频谱里“切一块窄带”，对这块做解调/解码/分析/录制/转发。  
> 所以：大多数 Channel 不需要额外硬件；你需要的是“能覆盖该频段的 SDR + 合适的天线”，少数测量类插件需要额外仪表/噪声源。 citeturn1view0

---

## 先给你一个“选天线/配件”的总规则

1) **决定一切的是频段**：同一个 HackRF，1090MHz（ADS‑B）好收，不代表 518kHz（Navtex）也行。  
2) **HackRF 的强项是 VHF/UHF/微波**；HF/LF 能听但“门槛更高”（天线、环境、前端、甚至上变频器/另一个 SDR）。  
3) **“能收到”与“解得出”**：很多数字模式要 SNR、频偏、动态范围；先在瀑布图看到“像样的信号形状”，再谈解码率。

---

## 1) 交通/导航类（最好玩、最直观）

### ADS‑B Demodulator（飞机应答机广播）
- **是什么**：解码 1090MHz ADS‑B 报文，显示航班/机型/速度/高度，并可联动地图。
- **常见频段**：1090MHz（最主流）；部分地区也有 978MHz UAT（这个插件是否覆盖取决于实现/配置，主流还是 1090）。
- **硬件/天线**：任何覆盖 1090MHz 的 SDR；**1090 专用天线**（或 1/4 波长约 6.9cm 的简易天线）效果提升巨大。
- **HackRF 适配**：能用，但比专用 ADS‑B 接收棒更“吃天线/摆位/增益”。（你已经验证 OK）
- **额外配件**：可选 LNA/滤波器（1090 带通）提升弱信号与抗干扰。

### ILS Demodulator（仪表着陆系统）
- **是什么**：接收并解调 ILS（Localizer/Glide Slope）导航信号，用于观察进近指引相关的调制分量。
- **频段**：Localizer 108.10–111.95MHz（与 VOR 频段相邻）；Glide Slope 在 UHF（约 329–335MHz，具体与台站配对）。
- **硬件/天线**：覆盖 VHF 航空导航段的 SDR；VHF 天线（或宽带天线）。
- **HackRF 适配**：可以。
- **额外配件**：无必需。

### VOR Demodulator（甚高频全向信标）
- **是什么**：解调 VOR 台站，用于观察方位信息（导航台“辐射的方位参考”）。
- **频段**：108.00–117.975MHz。 citeturn1view0
- **硬件/天线**：VHF 天线或宽带天线；位置越接近机场/导航台越容易。
- **HackRF 适配**：可以。
- **额外配件**：无必需。

### Frequency Scanner（频率扫描）
- **是什么**：在一个频率范围内扫频找“有信号的点”，并可触发把另一个 Channel（例如 AM/NFM/DSD）跳转到那个频点。 citeturn1view0
- **频段**：取决于你的扫描范围。
- **硬件/天线**：取决于你扫什么。
- **HackRF 适配**：可以（但扫得越宽越吃 CPU/采样率）。
- **额外配件**：无必需。

### Frequency Tracker（载波跟踪/自动跟频）
- **是什么**：跟踪某个载波中心频率的漂移，并把“跟踪后的频率”暴露给外部程序/脚本（Reverse API），用于联动控制其他插件。 citeturn1view0
- **适用场景**：温漂大的发射机、频偏较大的廉价设备、或需要自动对准中心的载波（某些数据链/遥测）。
- **额外配件**：无必需。

---

## 2) 广播/语音收听类（入门友好）

### AM Demodulator（调幅）
- **是什么**：收听 AM（例如中波广播、部分航空语音等）。 citeturn1view0
- **频段**：从中波到短波、乃至航空 AM（118–137MHz）都可能用 AM。
- **HackRF 适配**：航空 AM 很适合；中波/短波用 HackRF 也能玩但更挑天线/干扰环境。
- **额外配件**：HF 时可选上变频器、或换 Airspy HF+/RSP 等更适合 HF 的 SDR。

### NFM Demodulator（窄带调频）
- **是什么**：收听窄带 FM（对讲、业余、部分业务电台等）。 citeturn1view0
- **频段**：VHF/UHF 常见（例如 150/160/430/470MHz 等）。
- **HackRF 适配**：可以。
- **额外配件**：无必需。

### WFM Demodulator（宽带 FM“通用版”）
- **是什么**：宽带 FM 解调，带宽可到 250kHz；也能解 25k/12.5k 的窄带。 citeturn6search3
- **备注**：它不带广播 FM 那套（去加重/立体声/RDS）完整体验；听广播 FM 更推荐用 **Broadcast FM Demodulator**。 citeturn1view0turn6search3

### Broadcast FM Demodulator（广播 FM：立体声 + RDS）
- **是什么**：专门收听广播 FM（通常 88–108MHz），支持立体声与 RDS。 citeturn1view0
- **硬件/天线**：VHF 天线即可。
- **HackRF 适配**：可以。

### SSB Demodulator（单边带/DSB/CW）
- **是什么**：收听 SSB/DSB/CW（业余电台、短波通信等）。 citeturn1view0
- **频段**：多在 HF（1.8–30MHz）也可在 VHF/UHF。
- **HackRF 适配**：HF 能玩但不算强项；若你想认真玩短波，建议另备 HF 更强的 SDR 或上变频器。

### WDSP Receiver（“通信接收机”级别的 DSP）
- **是什么**：基于 WDSP（Warren Pratt, NR0V）的一套“高质量通信接收机”DSP 链路，提供更丰富的滤波/降噪/AGC 等处理，偏“玩音质/可懂度/弱信号”。 citeturn7search6
- **适用**：SSB/CW/语音类的“抠细节”。
- **硬件/天线**：取决于频段；插件本身不要求额外硬件。

---

## 3) 数字语音/数字通信类（注意合规）

> 提醒：很多数字语音/业务通信涉及隐私或受法律限制；请确保只接收你有权接收的内容，或用于公开/业余许可范围内的信号。

### DSD Demodulator（数字语音：DMR/D‑Star/YSF/NXDN…）
- **是什么**：数字语音解码器，覆盖多种常见数字语音制式（DMR、D‑Star、dPMR、YSF、NXDN 等）。 citeturn1view0
- **硬件/天线**：取决于信号在哪个频段（多在 VHF/UHF）；需要足够 SNR 和正确带宽。
- **额外依赖/硬件**：有些平台/编译方式会把 DSD 相关库作为“特殊条件”组件处理；某些情况下还会涉及 AMBE 硬件声码器（音质/兼容性），但不是所有场景都需要。 citeturn2search2

### FreeDV Demodulator（业余数字语音 FreeDV）
- **是什么**：FreeDV 数字语音解调/解码（基于 Codec2）。 citeturn1view0
- **频段**：常在 HF（也可在更高频段实验）。
- **HackRF 适配**：HF 同样更挑；但用来“体验模式”可以。

### M17 Demodulator（业余数字语音 M17）
- **是什么**：解调/解码 M17（开源数字语音协议，Codec2）。 citeturn1view0
- **频段**：常在 VHF/UHF 的业余段。
- **HackRF 适配**：可以。

### Packet Demodulator（AX.25/APRS 包通信）
- **是什么**：解码 AX.25/APRS 数据包，并可转发给 APRS Feature 做显示/上网关等。 citeturn1view0turn6search5
- **频段**：各地 APRS 频点不同（例如 144.390MHz 在北美很常见；国内常用频点可能不同）。
- **HackRF 适配**：可以。
- **额外配件**：无必需（可选更合适的 VHF 天线）。

### RTTY Demodulator（电传打字）
- **是什么**：解码 RTTY（常见于业余/气象/航海等历史悠久的数据模式）。
- **频段**：HF 常见，也可能在 VHF/UHF。
- **HackRF 适配**：HF 同样更挑。

### FT8 Demodulator（弱信号数字通信 FT8）
- **是什么**：解码 FT8（业余弱信号模式，15 秒时隙，能在很低 SNR 下完成联络）。 citeturn6search0
- **频段**：主要在 HF，也有 VHF/UHF 的 FT8 活动。 citeturn6search0
- **HackRF 适配**：能玩，但在 HF 上“可用≠舒服”；更推荐 HF 专用 SDR 或加上变频器+好天线。
- **额外配件**：无必需（但对频率稳定度、噪声环境、天线很敏感）。

---

## 4) 海事/气象/遥测类（很有“探索感”）

### AIS Demodulator（船舶自动识别系统）
- **是什么**：解码 AIS 船舶位置/航向等报文，可联动地图。 citeturn1view0
- **频段**：VHF 海事 AIS 通道（国际上常见 161.975MHz / 162.025MHz）。
- **硬件/天线**：VHF 天线；靠海/河道/港区更容易收。
- **HackRF 适配**：可以。

### DSC Demodulator（海事数字选择呼叫）
- **是什么**：解码 DSC（海事电台的短报文呼叫/遇险等预定义数字消息）。 citeturn1view0
- **频段**：海事 VHF/中波/短波都有 DSC 频道（具体依地区/业务）。
- **硬件/天线**：取决于你要收的频道。

### Navtex Demodulator（518kHz 海事航警/气象）
- **是什么**：解码 NAVTEX 文本播报（航行警告、气象预报等）。 citeturn1view0
- **频段**：全球常用 518kHz（还有 490kHz、4209.5kHz 等地区/语言频道）。
- **HackRF 适配**：这已经是 LF/MF 边缘，HackRF 能否顺利玩取决于环境与天线；通常需要更合适的长线/有源环形天线，甚至换更适合低频的 SDR。

### Inmarsat C Demodulator（海事/卫星短报文业务）
- **是什么**：解调 Inmarsat‑C 业务信号，用于接收相关数据。 citeturn1view0
- **频段**：L 波段卫星下行（大致在 1.5GHz 一带，具体业务频点依卫星/波束）。
- **硬件/天线**：L 波段天线（通常需要带一定方向性，面向卫星方向），最好低噪声放大（LNA）。
- **HackRF 适配**：频段覆盖没问题，但对天线/摆位更敏感。

### Radiosonde Demodulator（气象探空：RS41）
- **是什么**：解码 RS41 探空仪（气象气球）数据，每秒一帧，含位置/速度/气压温湿等，并可转发给 Radiosonde Feature 做曲线/轨迹/地图。 citeturn7search1
- **频段**：通常在 400–406MHz。 citeturn7search1
- **硬件/天线**：400MHz 附近天线；越接近放球点越容易。
- **HackRF 适配**：可以。

### End‑of‑Train Demodulator（列车尾部装置遥测）
- **是什么**：解码列车 End‑of‑Train（EOT）尾部装置发的遥测包（运动状态、制动压力、尾灯、电池等）。 citeturn7search0
- **频段/制式**：地区差异很大：如 457.9375MHz（北美/印度）、477.7MHz（澳大利亚）、450.2625MHz（新西兰）；FSK、1200 baud 等。 citeturn7search0
- **HackRF 适配**：可以（前提是你所在地区确实有该业务且在这些频点附近）。
- **合规**：这类通常属于业务通信，注意当地法规与隐私边界。

---

## 5) 测量/分析/记录/转发类（“工程味”）

### Channel Analyzer（通道分析仪）
- **是什么**：分析/可视化工具（频谱 + 示波/触发），特别适合看脉冲类信号的频谱与时域形状。 citeturn1view0
- **硬件/配件**：无必需；吃 CPU/GPU。

### Channel Power（通道功率）
- **是什么**：测通道功率（平均功率、峰值、最小峰值、脉冲平均功率等），在指定带宽内统计。 citeturn5view0
- **用途**：做场强对比、找最佳天线摆位、做简单功率监测/门限触发。
- **额外配件**：无必需。

### Heat Map（射频热力图）
- **是什么**：基于通道功率生成 RF 热力图（把不同位置/路线上的功率“画在地图上”）。 citeturn1view0
- **用途**：走动测覆盖、找干扰源大概方向、对比天线方案。
- **额外配件**：需要“位置信息来源”（电脑 GPS/手机共享/手动），否则只能做不带地理的统计。

### Noise Figure（噪声系数测量）
- **是什么**：用 Y‑factor 方法测接收机（以及可选 LNA）噪声系数，需要**校准噪声源**。 citeturn5view1
- **硬件/配件（这是少数必须额外硬件的）**：
  - 校准噪声源（带 ENR 标定数据）
  - 可能还需要可控电源/SCPI（取决于你怎么给噪声源上电）
  - 一些场景建议加 DC block（尤其当 SDR 有 Bias‑T 时）。 citeturn5view1

### Radio Astronomy（射电天文）
- **是什么**：做射电天文相关测量的一组工具（功率积分、漂移扫描、可能的频谱统计等）。 citeturn1view0
- **硬件/天线**：从“随便听听银河系噪声”到“认真做氢线”差距巨大；通常需要更好天线（抛物面/阵列）、LNA、滤波、稳定时钟等。
- **HackRF 适配**：可入门体验；认真玩建议更高动态范围/更低噪声的接收链路。

### Radio Clock（授时台：DCF77/MSF/WWVB…）
- **是什么**：解码授时台信号（例如 DCF77、MSF、TDF、WWVB）。 citeturn1view0
- **硬件/天线**：这些多在 **低频（几十 kHz）**，通常需要长波天线/有源磁环；HackRF 在这类低频上不占优，很多人用更适合 LF 的设备或专用接收器。
- **地区提示**：不同国家授时台不同，中国常见授时/标准频率体系也不同；能否收到取决于你所在地与台站覆盖。

---

## 6) “保存/喂给别的软件/跨机器跑”的工具类（很实用）

### File Sink（录制通道 IQ）
- **是什么**：把某个通道的 IQ 录下来（做离线回放、复现问题、分享样本）。 citeturn1view0
- **配件**：无；吃磁盘。

### SigMF File Sink（用 SigMF 规范录 IQ）
- **是什么**：录制为 SigMF 格式（通常含元数据），方便跨软件/跨平台共享与复现。 citeturn7search11
- **备注**：是否在你的 Windows 发布版里可用，取决于该构建是否包含这个插件；有些文档提到它在某些编译条件下才启用。 citeturn1view0turn7search11

### UDP Channel Sink（UDP 发样本）
- **是什么**：把通道样本用 UDP 发给别的程序（例如 GNU Radio 的 UDP Source），还能把 48kHz 音频回送混音。 citeturn1view0
- **配件**：无；需要对端程序/网络。

### Local channel sink（本机内部“走管道”）
- **是什么**：把通道 IQ 从一个 device set 送到另一个 device set 的 Local Input（不走网卡，进程内/本机内部管道）。 citeturn1view0
- **用途**：同一台机器里做“分层/分流”：一个设备源切多路、不同处理链各跑各的。

### Remote channel sink（UDP/网络远端）
- **是什么**：把通道 IQ 发到另一台 SDRangel（Remote Input）或远端处理实例。 citeturn1view0

### Remote TCP channel sink（TCP/rtl_tcp 兼容）
- **是什么**：把通道 IQ 通过 TCP 发出去；对端既可以是 SDRangel 的 Remote TCP Input，也可以是兼容 `rtl_tcp` 协议的软件。 citeturn7search4
- **用途**：把 SDRangel 当成“多硬件聚合 + 网络输出”的网关，让传统 `rtl_tcp` 客户端也能吃到 HackRF/其他 SDR 的数据。 citeturn7search4

---

## 7) 你截图里还有两个“看名字像通用工具”的

### Channel Analyzer / Channel Power / Heat Map 这类
- 共同点：不“解码内容”，而是帮你 **看**、**量**、**画**。
- 想快速提升上手速度：  
  - 先用 **Channel Power** 找到“增益/摆位/天线”最优的组合  
  - 再上对应的解调器（ADS‑B、AIS、Radiosonde…）  

---

## 最后：我建议你下一步怎么玩（按“投入/收益比”排序）

1) **AIS（如果你有机会去河边/湖边/港口）**：很直观、能联动地图。  
2) **Radiosonde（RS41）**：每天固定时间段更容易遇到，解出来的数据很“科学”。 citeturn7search1  
3) **VOR/ILS**：在机场周边能看到很漂亮的特征。  
4) **FT8/SSB**：如果你对短波有兴趣，可能需要更合适的 SDR 或上变频器与天线投入。 citeturn6search0

