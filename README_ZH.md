NanoKVM
======

<div align="center">

![](https://wiki.sipeed.com/hardware/assets/NanoKVM/introduce/NanoKVM_3.png)

<h3>
    <a href="https://wiki.sipeed.com/hardware/en/kvm/NanoKVM/introduction.html"> Quick Start </a>
    |
    <a href="https://cn.dl.sipeed.com/shareURL/KVM/nanoKVM"> Hardware </a>
</h3>

[English](./README.md) | 中文 | [日本語](./README_JA.md) | [한국어](./README_KO.md)

</div>

> Your NanoKVM Power by RISC-V !
> 如果您在使用过程中有任何问题或建议，请在这里提交 issue， 或在 [MaixHub Discussion](https://maixhub.com/discussion/nanokvm)告诉我们.

## 简介

Lichee NanoKVM 是基于 LicheeRV Nano 的 IP-KVM 产品，继承了 LicheeRV Nano的极致体积 和 强大功能。

Lichee NanoKVM 目前有三个版本：

* NanoKVM-Cube Lite 为基础版配置，适合 具有一定DIY能力的个人用户 和 有批量需求的企业用户。
* NanoKVM-Cube Full 为完整版配置，带精致外壳和完整配件，内置开机即用的系统镜像卡，推荐个人用户购买。
* NanoKVM-PCle 为全新形态，内置 PCle 挡板，可固定在机箱内部。NanoKVM-PCle 在 NanoKVM-Cube 基础上增加了可选的 WiFi 和 PoE 功能；拥有自家的 PCle 插槽，可从主板 PCle 插槽取电；另外有线连接（ETH）也更加稳定，满足更多专业需求。

<div align="center">

![NanoKVM-Cube](https://wiki.sipeed.com/hardware/zh/kvm/assets/NanoKVM/1_intro/NanoKVM_1.jpg)

![NanoKVM-PCIe](https://wiki.sipeed.com/hardware/assets/NanoKVM/introduce/NanoKVM-PCIe.png)

</div>

> 对于关注安全的用户，可以阅读此问题 [#301](https://github.com/sipeed/NanoKVM/issues/301)，您会找到有关所有安全问题的解释。GitHub 作为一个开放和透明的平台，为讨论所谓的“后门”担忧提供了空间。开源使产品更加安全！

## 项目结构

``` shell
├── kvmapp          # APP更新包
│   ├── jpg_stream  # 兼容从非常老的版本中直接更新
│   ├── kvm_new_app # 触发 kvm_system 更新必要组件
│   ├── kvm_system  # kvm_system 应用
│   ├── server      # NanoKVM 前后端应用
│   └── system      # 必要系统组件
├── server          # NanoKVM 后端
├── support         # 辅助功能(图像子系统、系统状态、系统更新、屏幕、按键……)
│   ├── sg2002      # NanoKVM-Lite/Full/PCIe
│   └── h618        # NanoKVM-Pro
├── web             # NanoKVM 前端
├── LICENSE
├── README_JA.md
├── README.md
├── README_ZH.md
└── CHANGELOG.md
```

## 参数

| 产品 | NanoKVM (Lite) | NanoKVM (Full) | PiKVM V4 |
| --- | --- | --- | --- |
| 计算单元                | LicheeRV Nano(RISCV) | LicheeRV Nano(RISCV) | CM4 (ARM) |
| 分辨率                  | 1080P @ 60fps | 1080P @ 60fps | 1080P @ 60fps |
| 视频编码                | MJPEG, H264 | MJPEG, H264 | MJPEG, H264 |
| 视频延迟                | 90～230ms | 90～230ms | 100～230ms |
| UEFI/BIOS               | ✓ | ✓ | ✓ |
| 模拟USB键鼠 | ✓ | ✓ | ✓ |
| 模拟USB存储 | ✓ | ✓ | ✓ |
| IPMI      | ✓ | ✓ | ✓ |
| Wake-on-LAN | ✓ | ✓ | ✓ |
| ETH | 100M/10M | 100M/10M | 1000M/100M/10M |
| ATX电源控制 | 无，用户可自行连接 | USB接口IO控制板 | RJ45接口IO控制板 |
| OLED显示 | 无，用户可自行扩展 | 128x64 0.96" white | 128x32 0.91" white |
| 外接串口 | 2路 | 2路 | 1路 |
| TF卡 | 无，用户自备 | 有，开机即用 | 有 |
| 扩展配件 | 无 | PoE | WiFi/LTE |
| 功耗 | 0.2A@5V | 0.2A@5V | Peak 2.6A@5V |
| 电源输入 | PC USB即可供电 | PC USB即可供电 <br> 也支持额外辅助供电 | 需要DC 5V 3A供电 |
| 散热 | 静音无风扇 | 静音无风扇 | 需要风扇主动散热 |
| 尺寸 | 23x37x15mm <br> ～1/30 PiKVM V4 体积 | 40x36x36mm <br/> ～1/7 PiKVM V4 体积 | 120x68x44mm |

![](https://wiki.sipeed.com/hardware/zh/kvm/assets/NanoKVM/1_intro/NanoKVM_2.jpg)

## NanoKVM 硬件平台

NanoKVM 基于 Sipeed [LicheeRV Nano](https://wiki.sipeed.com/hardware/zh/lichee/RV_Nano/1_intro.html) 核心板搭建，这部分硬件的规格书、原理图、尺寸图等均可在这里找到：[点击这里](http://cn.dl.sipeed.com/shareURL/LICHEE/LicheeRV_Nano)

NanoKVM Lite 由 LicheeRV Nano E 和 HDMItoCSI 小板构成，NanoKVM FULL 在 NanoKVM Lite 基础上增加 NanoKVM-A/B 板和外壳。HDMItoCSI板用于转换HDMI信号；NanoKVM-A 包含 OLED、ATX控制输出（TypeC接口形式）、辅助供电（TypeC接口）以及ATX开关机、复位按键；NanoKVM-B 一端连接A板，一端连接电脑ATX针脚，用于电脑的远程开关机。

NanoKVM 镜像在LicheeRV Nano SDK 和 MaixCDK 基础上构建，可以兼容使用 LicheeRV Nano 的资料，反之LicheeRV Nano 或其他 SG2002 产品无法使用KVM软件。如果您想在 LicheeRV Nano 或 MaixCam 上构建 HDMI输入相关应用，请与我们联系，以获得技术支持。

注: SG2002的256MB内存中, 目前划分105MB用于多媒体子系统, NanoKVM会在视频图像采集和处理中使用这部分内存.

* [NanoKVM-A 原理图](https://cn.dl.sipeed.com/fileList/KVM/nanoKVM/HDK/02_Schematic/SCH_RV_Nano_KVM_A_30111.pdf)
* [NanoKVM-B 原理图](https://cn.dl.sipeed.com/fileList/KVM/nanoKVM/HDK/02_Schematic/SCH_HDMI_MIPI_31011.pdf)
* [NanoKVM 镜像下载](https://github.com/sipeed/NanoKVM/releases/tag/NanoKVM)

## 购买渠道

* [Aliexpress(全球，除了美国和俄罗斯)](https://www.aliexpress.com/item/1005007369816019.html)
* [淘宝](https://item.taobao.com/item.htm?id=811206560480)
* [Preorder (其它不支持淘宝和速卖通的国家)](https://sipeed.com/nanokvm)

## 社区

* [MaixHub Discussion](https://maixhub.com/discussion/nanokvm)
* QQ group: 703230713
