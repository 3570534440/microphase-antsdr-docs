## E310 开箱检测

[[English]](../../../../../html/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E310_Reference_Manual/AntsdrE310_Unpacking_examination.html)

### ●1. 概述

E310 是一款面向创客和SDR爱好者同时也可以满足专业应用场景的软件无线电,支持70 MHz 到 6 GHz 的宽频段射频信号收发，既可以作为 USB 外设使用，也可以通过编程实现脱机运行。众多的开源项目支持和学习教程，让客户接触更多应用成为可能。

![e310](./ANTSDR_E310_Reference_Manual.assets/e310.jpg)

### ●2. 物品清单

感谢您购买微相科技有限公司的 ANTSDR 系列软件无线电平台，当您拿到ANTSDR E310（标准版）之后，打开配件包，其中应包含如下内容，

- ANTSDR 软件无线电: X1

- USB 数据线: X2 

- 短胶棒天线: X2

- 托盘天线: X1

- 读卡器: X1

- 网线: X1

- 32GB SD 卡 X1

打开包装后，开始开箱检查

### ●3. ANTSDR 驱动软件安装

接下来使用**pluto固件**收听广播。

ANTSDR E310出厂默认的固件是Pluto固件，无需改动。

如果您没有pluto固件，可以从github下载.[下载pluto固件](https://github.com/MicroPhase/antsdr-fw-patch/releases)。

E310 出厂时已将 Pluto 固件烧录到 QSPI 中。因此，使用 Pluto 固件相对简单。Pluto 固件默认 IP 地址为 **192.168.1.10** ，用户名和密码为 **root analog** ，波特率为 **115200** 。

设置启动模式的DIP开关在网口下方，在外壳的网口下方可以清晰的看到BOOT QSPI SD的字样。SD卡里的固件和E310的QSPI里的固件都是Pluto固件，无论用什么启动方式，都是Pluto固件。启动后会看到绿灯闪烁

### ● Windows 系统

[下载plutosdr驱动](https://wiki.analog.com/university/tools/pluto/drivers/windows)

[下载串口驱动](https://ftdichip.com/wp-content/uploads/2021/08/CDM212364_Setup.zip)

○1. 安装 Windows 驱动程序： CDM212364_Setup.exe 和 PlutoSDR-M2K-USB-Drivers.exe

将网线一端连接到ANTSDR，另一端连接到电脑。连接天线到rx1端口

![e310](./ANTSDR_E310_Reference_Manual.assets/E310_connect_.png)

○2. 之后您可以在计算机管理 -> 设备管理器中看到 plutoSDR 设备。

如果没有，请检查你的固件是否正确，你的驱动是否安装，你的USB OTG线序是否连接。

![e310](./ANTSDR_E310_Reference_Manual.assets/pluto_windows.png)

○3.在您电脑的网络适配器中，依次设置本机IP地址、子网掩码、网关。本机IP地址设置为与ANTSDR同一网段，例如192.168.1.100。子网掩码设置为255.255.255.0，默认网关设置为192.168.1.1。

○4. Antsdr设备IP为192.168.1.10，此时需要打开cmd窗口，ping 192.168.1.10

![e310](./ANTSDR_E310_Reference_Manual.assets/ping192168110.png)


○5. 收听广播

在 Windows 中运行 SDRSharp.exe 文件来收听广播
![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp.png)

Antsdr设备IP为192.168.1.10

![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp_connect.png)

连接成功后，选择广播频道，开始收听广播。

![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp_fm_plutosdr.png)

### ● Linux 系统

○1. pluto 固件默认 ip 为 **192.168.1.10**，将本地 ip 地址设置为 **192.168.1.100**，然后 **ping 192.168.1.100**。

![e310](./ANTSDR_E310_Reference_Manual.assets/linux_ping192.168.1.10.png)

○2. 您可以参考此链接来安装[libiio](https://wiki.analog.com/resources/eval/user-guides/ad-fmcdaq2-ebz/software/linux/applications/libiio#:~:text=Libiio%20is%20a%20library%20that%20has%20been%20developed,of%20software%20interfacing%20Linux%20Industrial%20I%2FO%20%28IIO%29%20devices.)

或者

您可以在以下位置找到安装 libiio 的详细步骤 [AntsdrE310 Gnurdio](./AntsdrE310_gnurdio_cn.md)


○3. 如果已经安装了libiio，执行iio_info -s

![e310](./ANTSDR_E310_Reference_Manual.assets/linux_iio_info_s.png)


可以通过千兆以太网或 USB OTG 连接。
打开 sdr++ 软件。
连接成功后，即可开始收听广播。

![e310](./ANTSDR_E310_Reference_Manual.assets/linux_sdr++.png)
