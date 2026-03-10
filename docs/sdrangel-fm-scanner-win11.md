# SDRangel 用 HackRF 扫 FM 广播台（Windows 11）速记

目标：不必把采样率硬拉到 20MSPS 覆盖整个 88–108MHz，也能快速“扫台 → 停台 → 直接收听”。

## 适用前提

- 输入设备已是 `HackRF`（左侧面板标题类似 `HackRF[0]`）
- 你能正常看到频谱/瀑布图（说明设备在跑）

## 1) 建议的 HackRF 起步设置（先稳后快）

FM 广播台通常很强，先避免过载：

- `RF Amp`：关（后面台弱再开）
- `LNA`：`8–16 dB`
- `VGA`：`8–16 dB`
- `DC`：开
- `IQ`：开

采样率不用太大：
- `SR`：`2.4–4.0 MSPS` 都可（够用；更大更吃 CPU）

## 2) 添加 Frequency Scanner Channel

在设备窗口顶部那排图标里点 `Add channels`：

- 选择 `Frequency Scanner`
- `Apply` → `Close`

## 3) Frequency Scanner 推荐参数（广播 FM）

在 `Frequency Scanner` 面板里把扫描范围设成：

- 起始频率：`88.0 MHz`
- 结束频率：`108.0 MHz`
- 步进（Step）：`100 kHz`（更细更慢；想快就用 `200 kHz`）
- 停留时间（Dwell/Delay）：先用 `100–300 ms` 级别（太短可能来不及稳定测功率）

触发策略（不同版本 UI 字段名略有差异）：
- 以 **功率阈值** 或 **峰值/平均功率** 作为“发现电台”的条件
- 发现后选择“停台/锁定”或“把频点发送给被控通道（tracker/receiver）”

> 小技巧：如果你所在区域台很密，阈值设高一点能减少误停；反之设低一点能多发现弱台。

## 4) 添加 Broadcast FM Demodulator（用来听台）

再 `Add channels`：
- 选择 `Broadcast FM Demodulator`
- `Apply` → `Close`

在 `Broadcast FM Demodulator` 里建议：
- `De-emphasis`：`50 µs`（国内/欧洲常用；设错会“刺/闷”）
- 立体声/RDS：按需打开

## 5) 把“扫描结果”接到“解调器”

不同 SDRangel 版本的联动方式可能叫：
- “Track/Follow”
- “Set frequency”
- “Use reverse API / Device control”

通用思路是：
1) Scanner 扫到一个频点并“锁定”
2) 将该频点设置到 `Broadcast FM Demodulator` 的中心频率（或让解调器跟随）

如果你找不到“自动联动”的选项，最笨但稳定的方法：
- Scanner 面板里看到一个好看的频点后，手动把设备中心频率（或解调器 Δf）改到那个频点

## 6) 音质不行/串台：先查是不是过载

典型过载现象：
- 噪声地板整体抬高
- 频谱里到处都是“假峰/互调”
- 听起来发糊、爆音、台间互串

处理顺序：
1) 关 `RF Amp`
2) 下调 `LNA`/`VGA`
3) 必要时加一个 `10–20 dB` 衰减器（台太强的城市很管用）

## 7) 想“一眼看全 FM 频段”的设置（可选）

如果你机器够强，也可以用宽频直接看：
- `SR` 设到 `20 MSPS`
- `CF` 设 `98 MHz`（覆盖 88–108）

但更推荐扫台：更省资源、体验更接近收音机。

