## E200 gnuradio 

[[English]](../../../../device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E310_Reference_Manual/AntsdrE310_gnurdio.html)

### ●1. 概述
[Gnuradio](https://www.gnuradio.org/) 是一个开源软件

[Gnuradio](https://www.gnuradio.org/) 是一个免费的软件开发工具包，提供信号处理模块用来实现软件定义的无线电和信号处理系统。它可以与外部 RF 硬件一起使用，以创建软件定义的无线电，或者在类似仿真的环境中无需硬件。它广泛用于业余爱好者，学术和商业环境，以支持无线通信研究和现实世界的无线电系统。

GNURadio 软件提供了构建和运行软件无线电或仅用于通用信号处理应用程序的框架和工具。GNURadio 应用程序本身通常称为“流程图”，它是连接在一起的一系列信号处理块，从而描述了数据流。这些流程图可以用 C++或 Python 编程语言编写。GNURadio 基础结构完全用 C++编写，而许多用户工具都是用 Python 编写的。

与所有软件定义的无线电系统一样，可重配置性是一个关键特性。不为特定硬件而设计，GNU Radio 开放的接口能够轻松地将用户自己地无线电设备接入到 GNU Radio 的生态当中。

### ●2.在ubuntu上安装libiio

不同Ubuntu版本有所不同，具体可以参考安装资料：[gnuradio install](https://wiki.analog.com/resources/tools-software/linux-software/gnuradio)

#### ○1.安装系统包

在安装Pluto SDR驱动之前，先安装所需的依赖包，在终端输入以下命令

```
sudo apt install libxml2 libxml2-dev bison flex cmake git libaio-dev libboost-all-dev
sudo apt install libusb-1.0-0-dev
sudo apt install libavahi-common-dev libavahi-client-dev
sudo apt install bison flex cmake git libgmp-dev
sudo apt install swig
sudo apt install liborc-dev
```

#### ○2. 安装libiio

您可以在 [github](https://github.com/analogdevicesinc/libiio) 上找到libiio的源码。

```
git clone -b v0.24 https://github.com/analogdevicesinc/libiio.git
cd libiio
mkdir build
cd build
cmake ../
make
sudo make install
cd ../..
```
#### ○3. 安装 libad9361-iio

```
git clone https://github.com/analogdevicesinc/libad9361-iio.git
cd libad9361-iio
mkdir build
cd build
cmake ../
make
sudo make install
cd ../..

```
### ●3. gnuradio 和 gr-iio

安装gnuradio

```
apt-get update
apt install gnuradio -y
ldconfig
```

安装完成后 ,查看安装的版本

```
gnuradio-companion -help
```

#### 安装 gr-iio

如果您安装的是gnuradio3.8则需要安装gr-iio。3.8+ 版 gr-iio 需要 liborc-dev

```
(sudo) apt install liborc-dev
```
从源代码构建并安装 gr-iio：

```
git clone -b upgrade-3.8 https://github.com/analogdevicesinc/gr-iio.git
cd gr-iio
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr ..
make 
sudo make install
cd ..
sudo ldconfig
```


对于 3.8 版本，请确保 gr-iio swig 接口已添加到您的 PYTHONPATH 中。否则，您将在 Python 中遇到导入错误。常用命令如下（取决于操作系统和安装位置）：

```
export PYTHONPATH=$PYTHONPATH:/usr/lib/python{PYTHON VERSION}/{site or dist}-packages
```
添加的路径是新安装的 iio 文件夹的位置。
对于 3.8.2 版本，无需执行其他步骤。


#### gnuradio3.10

如果您使用的是 Gnuradio 3.10 或更高版本，则 Gnuradio 本身的基础安装中已包含 gr-iio，无需再安装。

所有安装完成后，我们可以在终端中打开 Gnuradio 。

```
gnuradio-companion
```

### ●4. Using the Pluto blocks

进行前需要先使用 Pluto 固件，PLTUO 固件使用方法可在此处查看 [Unpacking examination](./AntsdrE310_Unpacking_examination_cn.md)

您可以在这里找到 antsdr gnuradio 示例：

[gnuradio demo](https://github.com/MicroPhase/gnu-radio-demo)

![e310](./ANTSDR_E310_Reference_Manual.assets/gnuradio_test.png)

#### ○通用

**IIO Context URI**: IP:192.168.1.10

**Buffer Size**: 内部缓冲区的大小（以样本为单位）。IIO 模块每次只能输入/输出一个包含样本的缓冲区

#### ○PlutoSDR source

○**RF Bandwidth(MHz)**: 配置 RX 模拟滤波器: RX TIA LPF 和 RX BB LPF.[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rx_rf_bandwidth_control)

○**Sample Rate(MSPS)**: 硬件每秒钟输入或输出采样数据的频率.[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#settingquerying_the_rx_sample_rate)

○**LO Frequency(MHz)**: 选择 RX 本振频率。范围：70MHz 至 6GHz，调谐精度：1Hz.[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#local_oscillator_control_lo)

○**Tracking**: [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#calibration_tracking_controls)

○Quadrature

○RF DC

○BB DC

○**Manual Gain(dB)**: 仅在手动增益控制模式 (MGC) 下控制 RX 增益. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#mgc_setting_the_current_gain)

○**Gain Mode**: 选择一种可用模式: manual, slow_attack, hybrid 和 fast_attack. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#gain_control_modes)

○**Filter**: 允许从文件加载 FIR 滤波器配置. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#digital_fir_filter_controls)

○**Filter auto** 启用后会加载默认滤波器，从而实现较低的 sampling / baseband rates.

![e310](./ANTSDR_E310_Reference_Manual.assets/PlutoSDR_source.png)

#### ○PlutoSDR sink

○**RF Bandwidth(MHz)**: 配置 TX 模拟滤波器: TX BB LPF and TX Secondary LPF. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#tx_rf_bandwidth_control)

○**Sample Rate(MSPS)**: 硬件每秒钟输入或输出采样数据的频率. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#settingquerying_the_tx_sample_rate)

○**LO Frequency(MHz)**: 选择 TX 本振频率。范围：70MHz 至 6GHz，调谐精度：1Hz. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#local_oscillator_control_lo)


○**RF Port Select**: 选择射频端口.[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rf_port_selection)

○**Attenuation (dB)**: 分别控制 TX1 和 TX2 的衰减。范围为 0 至 -89.75 dB，步长为 0.25 dB.[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#tx_attenuation_control)

○**Cyclic**: 如果需要“ Cyclic ”模式，请设置为“true”。在这种情况下，第一个缓冲区的样本将在 FMCOMMS-2 的已启用通道上重复，直到程序停止。

○**Filter**: 允许从文件加载 FIR 滤波器配置. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#digital_fir_filter_controls)

○**Filter auto** 启用后会加载默认过滤器，从而实现较低的 sampling / baseband rates.


![e310](./ANTSDR_E310_Reference_Manual.assets/plutosdr_sink.png)

### ●4. Using the fmcomms blocks

使用前，您需要使用 fmcomms 固件。您可以在此处找到 fmcomms 固件的使用方法 [fmcomms](./AntsdrE310_fmcomms_cn.md)

FMCOMMS-2 IIO 模块可以通过 IP 网络或 USB 运行。通过将“IIO context URI”参数设置为目标板的 IP 地址，您可以从远程传输样本。

![e310](./ANTSDR_E310_Reference_Manual.assets/gnuradio_fmcomms.png)

**IIO Context URI**: IP:192.168.1.10

**Buffer Size**: 内部缓冲区的大小（以样本为单位）。IIO 模块每次只能输入/输出一个包含样本的缓冲区

#### ○fmocmms source
○**RF Bandwidth(MHz)**: 配置TX模拟滤波器: TX BB LPF and TX Secondary LPF. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rx_rf_bandwidth_control)

○**Sample Rate(MSPS)**: 硬件每秒钟输入或输出采样数据的频率 . [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#settingquerying_the_rx_sample_rate)

○**LO Frequency(MHz)**: 选择TX本振频率。范围：70MHz至6GHz，调谐粒度：1Hz. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#local_oscillator_control_lo)

○**RF Port Select**: 选择要使用的 RF 端口. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rf_port_selection)

○**Tracking**: [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#calibration_tracking_controls)

○Quadrature

○RF DC

○BB DC

○**Manual Gain(dB)**:仅在手动增益控制模式 (MGC) 下控制 RX 增益.. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#mgc_setting_the_current_gain)

○**Gain Mode(RX1, RX2)**: 选择一种增益模式: manual, slow_attack, hybrid and fast_attack. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#gain_control_modes)

![e310](./ANTSDR_E310_Reference_Manual.assets/fmcomms_source.png)


#### ○fmocmms sink

○**RF Bandwidth(MHz)**: 配置TX模拟滤波器: TX BB LPF and TX Secondary LPF. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rx_rf_bandwidth_control)

○**Sample Rate(MSPS)**:  硬件每秒钟输入或输出采样数据的频率. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#settingquerying_the_rx_sample_rate)

○**LO Frequency(MHz)**: 选择TX本振频率。范围：70MHz 至 6 GHz，调谐精度：1Hz. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#local_oscillator_control_lo)

○**RF Port Select**: 选择要使用的RF端口. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#rf_port_selection)

**Attenuation(RX1, RX2)(dB)**: 别控制 TX1 和 TX2 的衰减。范围为 0 至 -89.75 dB，步长为 0.25dB。[Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#tx_attenuation_control)


○**Cyclic**: 如果需要“ Cyclic ”模式，请设置为“true”。在这种情况下，第一个缓冲区的样本将在 FMCOMMS-2 的已启用通道上重复，直到程序停止。

○**TX1/TX2** 使能: 启用传输数据路径

○**Filter**: 允许从文件加载 FIR 滤波器配置. [Read more](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-transceiver/ad9361#digital_fir_filter_controls)

○**Filter auto** 启用后会加载默认过滤器，从而启用较低的ampling / baseband rates.
![e310](./ANTSDR_E310_Reference_Manual.assets/fmcomms_source.png)

