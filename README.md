# PICO-Electronics 电气设计

[PICO-Humanoid](https://github.com/pico-humanoid/pico-humanoid.github.io) 的电气子项目，负责整机供电、MCU 底板、连接器与线束，以及与机械、固件共同完成装配和联调。

更新：2026-10-31。本文区分方案选定、设计检查和实物验证；器件参数不代表整机已达到相同指标。

## 当前进展

| 项目 | 已有结论 | 尚未完成或确认 |
| --- | --- | --- |
| 主电源 | 采用仓库所列 13S / 48V、12Ah 电池与 CAN BMS 方案 | 最新到货、铭牌、BMS 配置及负载能力核对 |
| 电源分配 | 采用 RobStride 电源板；提供电机动力支路和 24V、12V、5V 辅助输出 | 实际供电时序、急停、预充与泄放配置及负载验证 |
| 机载计算机 | 单独使用 48V→19V DC-DC 支路；团队已分享上电演示 | 实物型号、取电位置、负载电压及温升记录 |
| MCU 底板 | NUCLEO-G474RE + 三颗 TJA1051T/3；已整理三路 CAN、TVS、独立终端开关、提示电路 | 订单与最新设计对应、实板装配和功能验收 |
| PCB | 已有布局布线及 10/27 绕安装孔后的 DRC 通过记录；10/29 确认已下单等待到货 | 最新物流、裸板/贴片状态及下单文件是否包含最后绕孔修改 |
| CAN 基础实验 | 固件仓库已记录 G474 + SN65HVD230 + USB-CAN-A 的 FDCAN1 基础收发 | 新底板三路实测、真实关节/BMS/电源板查询、多节点和上下位机联调 |

19V 与主电源的团队上电演示只作为初步进展；新底板没有实物验收记录。详见[设计与验证记录](docs/设计与验证记录.md)。

## 供电方案

13S 电池经核对后的保护与电源管理路径向电机提供动力；电源板的 **5V/2A 输出为底板和 MCU 开发板供电**，机载计算机使用独立 19V 降压支路。底板的 J1 只接 5V 与 GND，不能接入 48V。

[整机供电与线束](power/供电方案.md) · [电池参数与核对事项](power/电池方案.md)

## PCB 方案

采用成品 NUCLEO-G474RE 开发板加自制双层底板，保留现有主体设计。底板提供三路独立 CAN 收发器，每路两个并联的 GH1.25 两针接口、TVS 和可独立投入的 120Ω 终端电阻；另有电源指示、可编程 LED 和蜂鸣器驱动。

[主板电路、引脚与器件作用](board/主板方案.md) · [PCB 布局布线与制造版本](board/PCB方案.md)

## 原首页三项问题的结论

| 原问题 | 当前结论 |
| --- | --- |
| 电池 BMS、电源板、电机多路 CAN 如何协调？ | 起步按 CAN1 接关节与电源板、1Mbit/s 规划；BMS 文档默认 500kbit/s，保持该配置时使用独立 CAN2；CAN3 预留。最终整机分路按负载、线束及实测调整。 |
| CAN 还是 CAN FD？ | 当前接入设备与联调按经典 CAN；关节和电源板采用 29 位扩展帧。G474 的 FDCAN 能力不代表当前整条链已支持或验证 CAN FD。 |
| 开发板上是否已有 CAN 收发器？ | NUCLEO-G474RE 提供 MCU 内部控制器，CANH/CANL 物理接口需要外接收发器。实验用 SN65HVD230；新底板用 TJA1051T/3，供电方法分别核对。 |

上述结论与[固件硬件文档](https://github.com/pico-humanoid/pico-firmware/blob/main/docs/hardware/README.md)、[通信方案](https://github.com/pico-humanoid/pico-firmware/blob/main/docs/communication/README.md)对齐。已选方案与已验证范围分别记录，剩余问题集中在[待确认与协作事项](docs/待确认与协作事项.md)。

## 接下来怎样推进

1. 先确认板子、电机和装配器件状态，核对制造版本、BOM 与固件引脚。
2. 板到后按断电检查、5V 控制侧上电、三路 CAN 台架测试的顺序验收。
3. 再与固件进行单设备只读查询、受限单关节测试、多节点及上下位机联调。

每步的准备、完成标准和记录内容见[装配、上电与联调](docs/装配上电与联调.md)。

## 资料入口

- [BOM 与采购记录](BOM/)：现有 1014 / 1016 / 1022 购买清单；不能直接代替最终底板装配 BOM。
- [器件与设备手册](datasheet/)：NUCLEO-G474RE、TJA1051、电源板 V1.5、嘉佰达 CAN 协议。
- [固件仓库](https://github.com/pico-humanoid/pico-firmware) · [机械仓库](https://github.com/pico-humanoid/pico-mechanism)
- [资料依据与版本记录](docs/设计与验证记录.md)：方案来源、设计检查范围与待归档资料。

嘉立创 PICO-Humanoid 团队入口沿用原仓库：
https://u.lceda.cn/join?type=team&key=3ae4fa2f6dcc287a4c28ea388aabda9c&inviter=3521a3620bad4043a5a4a711afc9a91c&team_uuid=f433dbb9b1824e4bb703ed7ed252efce
