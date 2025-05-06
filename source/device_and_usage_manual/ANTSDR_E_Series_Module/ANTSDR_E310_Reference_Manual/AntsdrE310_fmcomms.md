## E310 fmcomms

[[中文]](../../../cn/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E310_Reference_Manual/AntsdrE310_fmcomms_cn.html)

### ●1. Overview

ANTSDR FMCOMMS2/3/4 image can support 2t2r 61.44Msps sampling rate

### ●2. Download image 

First download the fmcomms firmware

[Download image-ADI-Kuiper-full.zip](https://wiki.analog.com/resources/tools-software/linux-software/adi-kuiper_images/release_notes)

[ADI AD-FMCOMMS3-EBZ User Guide](https://wiki.analog.com/resources/eval/user-guides/ad-fmcomms3-ebz#:~:text=The%20AD-FMComms3-EBZ%20is%20an%20FMC%20board%20for%20the,be%20found%20on%20the%20the%20ADI%20web%20site)

### ●3. fmcomms firmware 
### ●windows

After the user decompresses it, he can use the image burning tool to burn it to the SD card.

First, you need to prepare a 32GB SD card and format it to FAT32. The capacity of the SD card selected by the user should be larger than the size of the firmware.

[Download win32diskimager](https://sourceforge.net/projects/win32diskimager)

Among the provided materials, there is a tool for burning images, win32diskimager. Users can install the tool and then use it to burn images. Burning images on the Windows platform is very simple. Users only need to use the burning tool, select the .img image to be burned, and then select the SD card device to be burned, and then click Write to burn the image.
![e310](./ANTSDR_E310_Reference_Manual.assets/windows_win32diskimage.png)

After waiting for the burning to be completed, the user also needs to copy the files in the boot_file in the data to the BOOT partition of the SD card.


### ●linux
Burning images in Ubuntu

```
sudo dd if=2021-02-23-ADI-Kuiper.img of=/dev/sdb bs=1M
```
Among them, 2021-02-23-ADI-Kuiper.img is the location of the openwifi image after you unzip it, and sdb is the location where the SD card is mounted in the ubuntu system. Users can determine these two variables according to their actual environment. Then use the command in the above format to burn the image. After burning, you also need to copy the files in the boot_file folder to the BOOT partition of the SD card.

![e310](./ANTSDR_E310_Reference_Manual.assets/fmcomms_bootfile.png)

### ●How to set the IP address
After successfully burning the firmware, start antsdr and connect to the serial port. To successfully connect to the antsdr of the fmcomms firmware, you need to configure the network IP
```
sudo screen /dev/ttyUSB1 115200
```
/dev/ttyUSB1 is the uart serial port. If your serial port does not have any message, please check whether the board is started, check whether the serial port is correct, or whether the startup file is copied to the BOOT partition of the board.

Here I set the ANTSDR's Ethernet port to a static IP, so that it will get the same IP address every time it is powered on, making it easier to access the device in GNU Radio or libiio on the host computer. First open the /etc/network/interfaces file
```
vi /etc/network/interfaces
```
Then add the following settings in the file: Set the IP to 192.168.1.10
```
auto eth0
iface eth0 inet static
address 192.168.1.10
netmask 255.255.255.0
gateway 192.168.1.1
```
After adding, restart ANTSDR with the reboot command

Therefore, when using libiio to access the device, you only need to set the address. Here, the IP address of the network port connected to ANTSDR on the user's Linux host must be in the same network segment as ANTSDR. For example, the IP address of the author's computer host is 192.168.1.100. Then we can use libiio to test the connection.

If you don't have libiio installed, install libiio first

You can refer to this link to install [Libiio](https://wiki.analog.com/resources/eval/user-guides/ad-fmcdaq2-ebz/software/linux/applications/libiio#:~:text=Libiio%20is%20a%20library%20that%20has%20been%20developed,of%20software%20interfacing%20Linux%20Industrial%20I%2FO%20%28IIO%29%20devices.)

or

You can find detailed steps for installing libiio in [AntsdrE310 gnurdio](./AntsdrE310_gnurdio.html)


If you successfully installed libiio, execute iio_info -s

![e310](./ANTSDR_E310_Reference_Manual.assets/fmcomms_iio_info.png)

If you want to use the fmcomms firmware with gnuradio and connect to antsdr, have a look at **[Antsdr fmcomms](./AntsdrE310_gnurdio.html)**