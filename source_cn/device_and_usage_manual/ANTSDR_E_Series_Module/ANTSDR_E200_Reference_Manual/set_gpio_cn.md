## 设置gpio

[[English]](../../../../device_and_usage_manual/ANTSDR_E_Series_Module/ANTSDR_E200_Reference_Manual/set_gpio.html)


### Pluto Firmware
E200 有 8 个用户可操作的 GPIO。至于如何使用这 8 个 GPIO，可以使用下面的方法。在 Pluto 固件中使用 GPIO，就像直接操作 EMIO 一样。这种方法简单直接。
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
