# PICO-Electronics 电气设计

本仓库是 [PICO-Humanoid](https://github.com/pico-humanoid/pico-humanoid.github.io "访问项目主入口") 负责电气设计部分的子项目，主要涵盖电源方案、电路板设计等内容。

> 加入嘉立创 PICO-Humanoid 团队：
> https://u.lceda.cn/join?type=team&key=3ae4fa2f6dcc287a4c28ea388aabda9c&inviter=3521a3620bad4043a5a4a711afc9a91c&team_uuid=f433dbb9b1824e4bb703ed7ed252efce


## 供电方案

*Coming soon...*

## PCB 方案

*Coming soon...*


---

# 以下内容仅供设计参考


- 主电源
    - 电压：48V (13S)
    - 持续电流：40A（待定）
    - 峰值电流：80A（待定）
    - 输出端口：XT90S（待定，取决于电源板）
    - *其他数据待调研*
- 弱电源
    - 19V DC-DC
        - 供 Jetson Orin NX 使用
        - [参考商品](https://item.jd.com/10138079795809.html?pcdk=u330SRCgx35lDWlhAyD_OZFVwC-yGBpGtrJ5H8DzbxypaTGz2k9U0WP4V1iK2m8T.rQ4a.tlbT&spmTag=YTAyNDAuYjAwMjQ5My5jMDAwMDQwMjcuMyUyM3NrdV9jYXJkJTQwMTc5MTg4NTgwMDMzNiUyMzE4NDIwNjEwNiUyMzE3MzMwMDExMjE "访问“京东”")
    - 5V DC-DC
        - 供 MCU 及其他弱电设备使用
        - [参考商品](https://item.jd.com/10223872539848.html?extension_id=eyJhZCI6IjI2OCIsImNoIjoiMiIsInNrdSI6IjEwMjIzODcyNTM5ODQ0IiwidHMiOiIxNzkxODg1NTkwIiwidW5pcWlkIjoie1wiY2xpY2tfaWRcIjpcIjU1NjA5MmU5LWYzY2UtNGY4Mi1hZDExLTJhMzIxZTA3NWI5Y1wiLFwibWF0ZXJpYWxfaWRcIjpcIjc5OTk2NzQ2NTc4XCIsXCJwb3NfaWRcIjpcIjI2OFwiLFwic2lkXCI6XCIyNTA0YmY1Ni0zMmNmLTQzMjQtODk5NC1mZjNmOGFhMjg1YzNcIn0ifQ%3D%3D&jd_pop=556092e9-f3ce-4f82-ad11-2a321e075b9c&abt=0&pcdk=sZEKRLoJzNmrqGWR3qlhIMAUPQFZNMxRNPm0MqF3Z4Zqia7KWM5M5URTZtIT8HU6.rQ4a.tlbT "访问“京东”")
        
- 弱电替代方案：使用电源板？




### PCB-1：电源板

- **分电板作用：**
    - 将 48V 电池供电接口分为若干路 xt30(2+2) 电机电源线
    - 提供弱电DC-DC模块的输入接口
    - 电机CAN总线的集成
- 目前采用 [RobStride 电源板](power/供电方案.md)方案

### PCB-2：主板

- **主板作用：**
    - 接受 5V 供电，为核心板供电
    - 为核心板提供统一的电机 CAN 接口
    - （可选）提供其他指示信息（如LED、蜂鸣器等）

- MCU 采用成品开发板
    - [参考商品](https://item.jd.com/10111304966647.html?pcdk=PBjdioLsvdQBcw4EGL-Bf5d-9A2-k9vF4g_KkPEucaWSmB9sjVED6bxuDoMyTGDt.3z6a.aI3x&spmTag=YTAyMTkuYjAwMjM1Ni5jMDAwMDcyMTAua2V5d29yZF9lbnRlciU0MDE3OTIwMzcxMDE0MTAlMjMxNzkyMDM2OTQ2MTA4OTM3MjEwNTc0JTIzMTQ0NjI1OTc3MCUyQ2EwMjQwLmIwMDI0OTMuYzAwMDA0MDI3LjIlMjNza3VfY2FyZCU0MDE3OTIxMTk5MDg0OTUlMjMxNzkyMDM2OTQ2MTA4OTM3MjEwNTc0JTIzMTg3Mzc5ODA3OQ)
    - [数据手册](NUCLEO-G474REm32g4-nucleo64-boards-mb1367-stmicroelectronics.pdf)
    - 依据 MCU 排针布局设计主板排母

        <img src="assets/mcu.png" alt="MCU" height="400">

