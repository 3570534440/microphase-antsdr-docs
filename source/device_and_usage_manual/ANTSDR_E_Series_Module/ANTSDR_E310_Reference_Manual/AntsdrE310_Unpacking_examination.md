## E310 Unpacking examination


[[中文]](../../../cn/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E310_Reference_Manual/AntsdrE310_Unpacking_examination_cn.html)


### 1. Overview

The E310 is a software-defined radio (SDR) designed for makers and SDR enthusiasts while also meeting professional application requirements. It supports wideband RF signal transmission and reception across 70 MHz to 6 GHz, functioning either as a USB peripheral or operating offline through programming. Backed by extensive open-source projects and learning resources, it empowers users to explore diverse applications.

![e310](./ANTSDR_E310_Reference_Manual.assets/e310.jpg)

### 2. Package Contents

Thank you for purchasing the ANTSDR series SDR platform from MicroPhase Technology. Upon receiving your ANTSDR E310 (Standard Edition), open the accessory kit, which should include the following items:

- ANTSDR SDR Device: X1

- USB data cable: X2 

- Short rubber stick antenna: X2

- Tray antenna: X1

- Card reader: X1

- Network cable: X1

- 32GB SD card: X1

After unpacking, please check all items.

### 3. ANTSDR Device Software Installation 

Next, use the **Pluto firmware** to receive radio broadcasts.

The factory default firmware of ANTSDR E310 is Pluto firmware, no need to change.

If you don't have the Pluto firmware, it can be downloaded from github: [download ANTSDR Pluto firmware](https://github.com/MicroPhase/antsdr-fw-patch/releases)

E310 has burned the Pluto firmware into QSPI when it leaves the factory. Therefore, using the Pluto firmware is a relatively simple matter. The default IP address of the Pluto firmware is `192.168.1.10`. The username is `root`, and the password is `analog`.The baud rate is `115200`.

The DIP switch for setting the boot mode is under the network port.  you can clearly see the words BOOT QSPI SD under the network port of the shell. The firmware in the SD card and the firmware in the QSPI of E310 are both Pluto firmware, no matter what boot method is used, they are all Pluto firmware. When you power on, you will see a flashing green light.

#### ● Windows 

[Download PlutoSDR Drivers](https://wiki.analog.com/university/tools/pluto/drivers/windows)

[Download Serial Drivers](https://ftdichip.com/wp-content/uploads/2021/08/CDM212364_Setup.zip)

○1. Install Windows drivers： **CDM212364_Setup.exe** and **PlutoSDR-M2K-USB-Drivers.exe**.
Then, connect one end of the network cable to the ANTSDR device and the other end to your computer. Connect the antenna to the rx1 port
![e310](./ANTSDR_E310_Reference_Manual.assets/E310_connect_.png)
○2. After that you can see the plutoSDR device in Computer Management -> Device Manager .

If not, please check whether your firmware is correct, whether your driver is installed, and whether your USB OTG line sequence is correct.

![e310](./ANTSDR_E310_Reference_Manual.assets/pluto_windows.png)

○3. Configure the local IP address, subnet mask, and default gateway. Ensure the local IP address is within the same subnet as the ANTSDR, for example: `192.168.1.100`. Set the subnet mask to `255.255.255.0` and the default gateway to `192.168.1.1`.

○4. The ANTSDR device IP is 192.168.1.10. At this time, you need to open the cmd window and ping 192.168.1.10
![e310](./ANTSDR_E310_Reference_Manual.assets/ping192168110.png)


○5. Receive Broadcasts

Run SDRSharp.exe file in Windows to listen to the radio
![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp.png)

The ANTSDR device IP is `192.168.1.10`

![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp_connect.png)

Once connected, select a radio frequency channel to begin listening.

![e310](./ANTSDR_E310_Reference_Manual.assets/sdrsharp_fm_plutosdr.png)

#### ● Linux

○1. The default IP address of the Pluto firmware is `192.168.1.10`. Set your local IP address to `192.168.1.100`, and then ping `192.168.1.10` to check the connection.

![e310](./ANTSDR_E310_Reference_Manual.assets/linux_ping192.168.1.10.png)

○2. You can refer to this link to install **[libiio](https://wiki.analog.com/resources/eval/user-guides/ad-fmcdaq2-ebz/software/linux/applications/libiio#:~:text=Libiio%20is%20a%20library%20that%20has%20been%20developed,of%20software%20interfacing%20Linux%20Industrial%20I%2FO%20%28IIO%29%20devices.)**

or

You can find detailed steps for installing **libiio** in [ANTSDR E310 GNU Rdio](./AntsdrE310_gnurdio.md)


○3. If you have already installed **libiio**, Execute iio_info -s

![e310](./ANTSDR_E310_Reference_Manual.assets/linux_iio_info_s.png)

Can be connected via Gigabit Ethernet or USB OTG. 
Open the sdr++ software. 
After the connection is successful, you can start listening to the radio.


![e310](./ANTSDR_E310_Reference_Manual.assets/linux_sdr++.png)
