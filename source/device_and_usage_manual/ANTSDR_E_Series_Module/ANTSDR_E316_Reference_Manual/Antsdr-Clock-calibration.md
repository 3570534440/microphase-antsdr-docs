## Antsdr Clock calibration
Users need to enter the system to operate the iio device file, or access the iio device named ad5660mp through the libiio interface on the host computer. Here, the clock is calibrated by entering the system.

You need to prepare a 10M clock before use

![e310](./ANTSDR_E310_Reference_Manual.assets/microphase-10M.png)

Prepare SMA to MMCX cable

![e310](./ANTSDR_E310_Reference_Manual.assets/e310-10m-pps.png)

Before proceeding

Connect the SMA to MMCX cable to the 10/PPS port of antsdr

### ad5660mp

First, log into the system through the serial port, with the device user name root and password analog.

```
ant login: root
Password: 
Welcome to:
    ___    _   _____________ ____  ____ 
   /   |  / | / /_  __/ ___// __ \/ __ \
  / /| | /  |/ / / /  \__ \/ / / / /_/ /
 / ___ |/ /|  / / /  ___/ / /_/ / _, _/ 
/_/  |_/_/ |_/ /_/  /____/_____/_/ |_|  
                                       
v0.39-1-g7bcc-dirty
https://github.com/MicroPhase/antsdr-fw-patch

```
You can view the iio device by using the following command: iio_attr -d
```
iio_attr -d
```
You can see that there is an iio device called ad5660mp. Next, enter this file.
```
# cd /sys/bus/iio/devices/iio:device0
# ls
in_voltage_dac_locked      name
in_voltage_dac_mode        of_node
in_voltage_dac_read_value  power
in_voltage_dac_ref_sel     subsystem
in_voltage_dac_value       uevent
in_voltage_raw             waiting_for_supplier

```
You can see the following properties. Next, we will introduce the functions of the following properties.
```
in_voltage_dac_mode         0: Automatic setting. 1: Manual setting. Default is 1
in_voltage_dac_value        Write the value of dac
in_voltage_dac_read_value   Mode 1 User set DAC value Mode 0 External reference calibrated DAC value (23000)
in_voltage_dac_ref_sel      0:10M 1:PPS 2:GPS 
in_voltage_dac_locked       PLL lock status
```
The default state is manual setting, you can view the command through cat. The default is manual mode and the dac value is 23000.

```
# cat in_voltage_dac_mode
1
# cat in_voltage_dac_read_value
23000

```
### Automatic settings
10M automatic lock configuration, enter the following command to configure dac to automatic state 10M lock, this way When writing, execute one by one, press Ctrl+C after entering the return to exit, and you can use the cat command to check whether the setting is successful.
```
echo 0 > in_voltage_dac_mode
echo 0 > in_voltage_dac_ref_sel

```
PPS automatic lock configuration
```
echo 0 > in_voltage_dac_mode
echo 1 > in_voltage_dac_ref_sel
```
GPS auto lock configuration
```
echo 0 > in_voltage_dac_mode
echo 2 > in_voltage_dac_ref_sel
```
Wait for tens of seconds.After locking, you can view it through cat in_voltage_dac_locked.
```
# cat in_voltage_dac_locked 
1
```
### Manual settings

Manually set the mode and write the value.
```
echo 1 > in_voltage_dac_mode
echo 23000 > in_voltage_dac_value
```