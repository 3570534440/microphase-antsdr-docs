## Set GPIO

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
