# Hackintosh-ASUS-ROG-STRIX-Z490-A-GAMING-I910900K-6800XT
[![OpenCore](https://img.shields.io/badge/OpenCore-0.8.7-1ac3d4)](https://github.com/acidanthera/OpenCorePkg/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-13.0.1-ffb84a)](https://www.apple.com/macos/ventura/)

Hackintosh EFI For ASUS-ROG-STRIX-Z490-A-GAMING(吹雪)

华硕 Z490-A 吹雪 黑苹果 Opencore EFI

作为主力机使用，将持续更新，可以🌟Star一下～

---
## 软件版本

<img src="https://rog.asus.com/websites/global/products/enapehclupql13s5/img/z490/kv/hero.png" align="right" width="360" />

Bootloader: [OpenCore-0.8.7-RELEASE](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.8.7)

OS: [macOS Ventura 13.0.1](https://www.apple.com/macos/ventura/) (iMac20,2)

BIOS.Version: [2601](https://rog.asus.com.cn/motherboards/rog-strix/rog-strix-z490-a-gaming-model/helpdesk_bios/)

---

## 硬件配置

|    组件    |                  名称                   |
|:----------:|:---------------------------------------:|
|    主板    |      ASUS ROG STRIX Z490-A GAMING       |
| 中央处理器 |                I9 10900K                |
|    显卡    |   Intel UHD630 / AMD Radeon RX 6800XT   |
|    内存    | G.SKILL Trident Z Royal DDR4 4000 16Gx4 |
|    硬盘    |        Samsung 970 EVO Plus NVMe        |
| 蓝牙/WI-FI |          Fevi T919 BCM94360CD           |

### 板载配置详情

| 组件 |               名称                |
|:----:|:---------------------------------:|
| 网卡 | Intel I225-V 2.5 Gigabit Ethernet |
| 声卡 |         Realtek ALCS1220A         |

---

## 可正常工作
- [x] 显卡 (Intel UHD630 核显 + AMD Radeon RX 6800XT 独显) / 硬解 4K (HEVC + H.264)
- [x] Audio Realtek ALCS1220A 声卡 (板载)
- [x] Intel I225-V 2.5 Gigabit Ethernet 网卡 (板载)
- [x] Wi-Fi/BT (Fenvi T919 BCM94360CS PCIEX1)
- [x] USB 定制 (UTBMap + USBToolBox)
- [x] 重启/关机
- [x] 睡眠/唤醒
- [x] 电源管理 (原生)

---

## EFI详情

### GPU
#### AMD Radeon RX 6800XT (dGPU)

* 原生防黑屏启动参数

```
agdpmod=pikera
```

* 设备属性仿冒设置

```
    <key>DeviceProperties</key>
    <dict>
        <key>Add</key>
        <dict>
            <key>这里写你显卡的实际的设备路径(Hackintool PCIE里面可以看到)</key>
            <dict>
                <key>@0,name</key>
                <string>ATY,Belknap</string>
                <key>@1,name</key>
                <string>ATY,Belknap</string>
                <key>@2,name</key>
                <string>ATY,Belknap</string>
                <key>@3,name</key>
                <string>ATY,Belknap</string>
                <key>device_type</key>
                <string>ATY,BelknapParent</string>
            </dict>
        </dict>
        <key>Delete</key>
        <dict/>
    </dict>
```

* 温度传感器介入

使用 [RadeonSensor](https://github.com/aluveitie/RadeonSensor)

#### I9 10900K Intel UHD630 (iGPU)

* 采用白苹果iMac默认调度策略，核显仅用于计算，不驱动显示
  
DeviceProperties

|         key         |     value      | dataType |
|:-------------------:|:--------------:|:--------:|
| AAPL,ig-platform-id | **`0300C89B`** |   DATA   |
|      device-id      | **`9B3E0000`** |   DATA   |

* BIOS设置: DVMT Pre-Allocated: 64MB

### 声卡

#### Audio Realtek ALCS1220A

* 采用 [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases)

* 启动参数

```
alcid=layout-id // 我的layout-id为2
```

### 网卡

#### Intel I225-V 2.5 Gigabit Ethernet

最新Ventura 13.0更改为采用AppleIntelI210Ethernet.kext驱动I225-V网卡，删除DeviceProperties相关参数

* 启动参数

```
e1000=0
```