## Set Firmware IP

[[中文]](../../../cn/device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E200_Reference_Manual/set_gpio_cn.html)

The E200 has eight user-accessible GPIOs.

### Pluto Firmware
E200 has eight user-operable gpio. As for how to use these eight gpio, you can use the following method. Use gpio in pluto firmware, just like directly operating emio to operate it. This method is simple and direct.
```
#!/bin/bash

START=995
END=1002

for i in $(seq $START $END); do
  echo $i > /sys/class/gpio/export 2>/dev/null
  echo out > /sys/class/gpio/gpio$i/direction
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

When you use the UHD firmware, there are also 8 user-operable GPIOs. If you want to use these 8 GPIOs, you can refer to the following code
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