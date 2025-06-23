## Set Firmware IP

[[中文]](../../../cn/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E200_Reference_Manual/set_gpio.html)


### Pluto Firmware
E200 有 8 个用户可操作的 GPIO。至于如何使用这 8 个 GPIO，可以使用下面的方法。在 Pluto 固件中使用 GPIO，就像直接操作 EMIO 一样。这种方法简单直接。
```
#!/bin/bash

START=995
END=1002

for i in $(seq $START $END); do
  echo $i > /sys/class/gpio/export 2>/dev/null
  echo out > /sys/clhttps://microphase-antsdr-docs.readthedocs.io/en/latest/About_Us/About%20Us.html#contact-usass/gpio/gpio$i/direction
done

echo "Flip 995~1002..."

while true; do
  for i in $(seq $START $END); do
    echo 1 > /sys/class/gpio/gpio$i/value
  done
  sleep 0.5
  for i in $(seq $START $END); do
    echo 0 > /sys/class/gpio/gpio$i/value
  done
  sleep 0.5
done
```
### UHD firmware
当您使用uhd固件的时候，也有8个用户可以操作的gpio，如果您要使用这8个gpio，您可以参考下面的代码,该使用方法和uhd官方的使用方法没有区别
```
    std::cout << "Using GPIO bank: FP0 "<< std::endl;

    usrp->set_gpio_attr("FP0", "DDR", 0xff, 0xff); 
    // set control register 
    usrp->set_gpio_attr("FP0", "CTRL", 0, 0xff);   

    while (1) {
        usrp->set_gpio_attr("FP0", "OUT", 0xFF, 0xFF);  
        std::this_thread::sleep_for(std::chrono::seconds(1));
        uint32_t rb = usrp->get_gpio_attr("FP0", "READBACK");
        std::cout << "READBACK: " << std::hex << rb << std::endl;

        usrp->set_gpio_attr("FP0", "OUT", 0x00, 0xFF); 
        std::this_thread::sleep_for(std::chrono::seconds(1));
        rb = usrp->get_gpio_attr("FP0", "READBACK");
        std::cout << "READBACK: " << std::hex << rb << std::endl;
    }
```