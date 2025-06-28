## E316 Unboxing and Inspection
[[中文]](../../../cn/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E316_Reference_Manual/AntsdrE316_Unpacking_examination_cn.html)

### 1. Overview

The E316 is a software-defined radio (SDR) designed for professional applications, supporting wideband RF signal transmission and reception from 70 MHz to 6 GHz. It can operate as a USB peripheral or run standalone via programmable control. After two generations of refinement, the E316 features enhanced transmit power, improved receive sensitivity, lower noise floor and phase noise, and a more comprehensive wireless application interface. ANTSDR has accumulated a wealth of successful application cases in fields such as spectrum monitoring, UAVs, GPS, and radio signal analysis.

![E316](./AntsdrE316_Unpacking_examination.assets/E316-1750413194179-10.jpg)

### 2. Package Contents

Thank you for purchasing the ANTSDR series SDR platform from Weixiang Technology Co., Ltd.
Upon receiving your ANTSDR E316 (Standard Edition), please open the accessory pack. The following items should be included:

- ANTSDR Software-Defined Radio: ×1
- USB Data Cables: ×2
- Rubber Antennas: ×2
- Tray Antenna: ×1
- Ethernet Cable: ×1
- 32GB SD Card X1

### 3. Listen to the radio using **Pluto firmware**

The DIP switch for selecting the boot mode is located below the Ethernet port and is labeled "BOOT/QSPI/SD".
ANTSDR E316 comes pre-installed with Pluto firmware in QSPI memory. QSPI boot is Pluto firmware, SD card boot is UHD firmware

When the device boots successfully, the green status LED will flash.

If Pluto firmware is not installed on the device ，You can download and burn it from [GitHub Download](https://github.com/MicroPhase/antsdr-fw-patch/releases).

The default configuration of Pluto firmware is as follows:

- **IP Address**: 192.168.1.10
- **Username / Password**: root / analog
- **Baud Rate**: 115200

#### ● Windows 

[Download PlutoSDR Drivers](https://wiki.analog.com/university/tools/pluto/drivers/windows)

[Download Serial Drivers](https://ftdichip.com/wp-content/uploads/2021/08/CDM212364_Setup.zip)

○1. Install Windows drivers： **CDM212364_Setup.exe** and **PlutoSDR-M2K-USB-Drivers.exe**.

Then, connect one end of the network cable to the ANTSDR device and the other end to your computer. Connect the antenna to the RX1 port.


![e310](./AntsdrE316_Reference_Manual.assets/E316_connect.png)

○2. 之后，您可以在 **计算机管理 → 设备管理器** 中看到 **PlutoSDR** 设备。

如果未显示设备，请检查以下项是否正确：

- 固件是否烧录成功
- 驱动程序是否已正确安装
- USB OTG 是否正确插入

![e310](./AntsdrE316_Unpacking_examination.assets/pluto_windows.png)

○3.在您电脑的网络适配器中，依次设置本机IP地址、子网掩码、网关。本机IP地址设置为与ANTSDR同一网段，例如 `192.168.1.100` 。子网掩码设置为 `255.255.255.0` ，默认网关设置为 `192.168.1.1` 。

○4. ANTSDR 设备 IP 为 `192.168.1.10`，此时需要打开**CMD**窗口，`ping 192.168.1.10`

![e310](./AntsdrE316_Unpacking_examination.assets/ping192168110.png)


○5. 收听广播

在 Windows 中运行 **SDRSharp.exe** 文件来收听广播
![e310](./AntsdrE316_Unpacking_examination.assets/sdrsharp.png)

ANTSDR设备IP为`192.168.1.10`

![e310](./AntsdrE316_Unpacking_examination.assets/sdrsharp_connect.png)

连接成功后，选择广播频道，开始收听广播。

![e310](./AntsdrE316_Unpacking_examination.assets/sdrsharp_fm_plutosdr.png)

#### ● Linux 系统

○1. Pluto 固件默认 IP 为 `192.168.1.10`，将本地 IP 地址设置为 `192.168.1.100`，然后 `ping 192.168.1.100` 。

![e310](./AntsdrE316_Unpacking_examination.assets/linux_ping192.168.1.10.png)

○2. 关于 **libiio** 的安装，请参阅 [官方指南](https://wiki.analog.com/resources/eval/user-guides/ad-fmcdaq2-ebz/software/linux/applications/libiio)，或参考[《E310 GNU Radio》](./AntsdrE316_gnurdio.md)。


○3. 如果已经安装了 **libiio** ，执行`iio_info -s`

![e310](./AntsdrE316_Unpacking_examination.assets/linux_iio_info_s.png)

可以通过千兆以太网或 USB OTG 连接。
打开 **SDR++** 软件,适当调整增益。
连接成功后，即可开始收听广播。

![e310](../ANTSDR_E310_Reference_Manual/ANTSDR_E310_Reference_Manual.assets/linux_sdr++.png)
