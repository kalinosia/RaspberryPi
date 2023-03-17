What's your vector, Victoria? With the BNO085 you're HEADING in the right direction

# Overview

![obraz](https://user-images.githubusercontent.com/57706343/225981607-cd9fb325-ea4b-4aad-bd34-c16e0a29bed6.png) 
![obraz](https://user-images.githubusercontent.com/57706343/225981654-575de63d-8a02-4afe-8a69-976fa2c564e3.png)

> [!NOTE]
> Information the user should notice even if skimming.

Here it is, the motion sensor you were looking for: the one that just gives you the directly usable information without requiring you to first consult with a PhD to learn the arcane arts of Sensor Fusion. The BNO085 takes the life's work of multiple people who have spent their entire career focused on how to get useful information from direct motion sensor measurements and then squeezes that information down into a 5.2x3.8mm box, along with the sensors to go along with it.


-    **Acceleration Vector / Accelerometer**

      Three axes of acceleration (gravity + linear motion) in m/s^2
     
-    **Angular Velocity Vector / Gyro**

     Three axes of 'rotation speed' in rad/s
    
-    **Magnetic Field Strength Vector / Magnetometer**

     Three axes of magnetic field sensing in micro Tesla (uT)
    
-    **Linear Acceleration Vector**

     Three axes of linear acceleration data (acceleration minus gravity) in m/s^2
    
-    **Gravity Vector**

     Three axes of gravitational acceleration (minus any movement) in m/s^2
    
-    **Absolute Orientation / Rotation Vector**

     Four-point quaternion output for accurate data manipulation

### Interesting

> It's easy to use the BNO08x with Python or CircuitPython, and the Adafruit CircuitPython BNO08x module. This module allows you to easily write Python code that reads humidity and temperature from the BNO08x sensor. https://github.com/adafruit/Adafruit_CircuitPython_BNO08x

# Python Computer Wiring

![obraz](https://user-images.githubusercontent.com/57706343/225978226-1344872a-8c34-4c54-af3e-b832c1227514.png)


-    Pi 3V to sensor VCC (red wire)
-    Pi GND to sensor GND (black wire)
-    Pi SCL to sensor SCL (yellow wire)
-    Pi SDA to sensor SDA (blue wire)



> **I add this, not know if working good:**
> 
> NOTE: The BNO85 seems to work best on the Raspberry Pi with an I2C clock frequency of 400kHz. You can make that change by adding this line to your /boot/config.txt file:
>```
>dtparam=i2c_arm_baudrate=400000
>```

# Python Installation of BNO08x Library

`sudo pip3 install adafruit-circuitpython-bno08x`

# CircuitPython & Python Usage

Work in consol 

in python

### I2C Initialization

```
import time
import board
import busio
import adafruit_bno08x
from adafruit_bno08x.i2c import BNO08X_I2C

i2c = busio.I2C(board.SCL, board.SDA, frequency=800000)
bno = BNO08X_I2C(i2c)
```

### Enable the Rotation Vector/Quaternion Report

```
bno.enable_feature(adafruit_bno08x.BNO_REPORT_ROTATION_VECTOR)
```

### Check

```
print("Rotation Vector Quaternion:")
quat_i, quat_j, quat_k, quat_real = bno.quaternion
print(
  "I: %0.6f  J: %0.6f K: %0.6f  Real: %0.6f" % (quat_i, quat_j, quat_k, quat_real)
)
```

# Example code

test.py

```
# SPDX-FileCopyrightText: 2020 Bryan Siepert, written for Adafruit Industries
#
# SPDX-License-Identifier: Unlicense
import time
import board
import busio
from adafruit_bno08x import (
    BNO_REPORT_ACCELEROMETER,
    BNO_REPORT_GYROSCOPE,
    BNO_REPORT_MAGNETOMETER,
    BNO_REPORT_ROTATION_VECTOR,
)
from adafruit_bno08x.i2c import BNO08X_I2C

i2c = busio.I2C(board.SCL, board.SDA, frequency=400000)
bno = BNO08X_I2C(i2c)

bno.enable_feature(BNO_REPORT_ACCELEROMETER)
bno.enable_feature(BNO_REPORT_GYROSCOPE)
bno.enable_feature(BNO_REPORT_MAGNETOMETER)
bno.enable_feature(BNO_REPORT_ROTATION_VECTOR)

while True:

    time.sleep(0.5)
    print("Acceleration:")
    accel_x, accel_y, accel_z = bno.acceleration  # pylint:disable=no-member
    print("X: %0.6f  Y: %0.6f Z: %0.6f  m/s^2" % (accel_x, accel_y, accel_z))
    print("")

    print("Gyro:")
    gyro_x, gyro_y, gyro_z = bno.gyro  # pylint:disable=no-member
    print("X: %0.6f  Y: %0.6f Z: %0.6f rads/s" % (gyro_x, gyro_y, gyro_z))
    print("")

    print("Magnetometer:")
    mag_x, mag_y, mag_z = bno.magnetic  # pylint:disable=no-member
    print("X: %0.6f  Y: %0.6f Z: %0.6f uT" % (mag_x, mag_y, mag_z))
    print("")

    print("Rotation Vector Quaternion:")
    quat_i, quat_j, quat_k, quat_real = bno.quaternion  # pylint:disable=no-member
    print(
        "I: %0.6f  J: %0.6f K: %0.6f  Real: %0.6f" % (quat_i, quat_j, quat_k, quat_real)
    )
    print("")

```



> https://learn.adafruit.com/adafruit-9-dof-orientation-imu-fusion-breakout-bno085/python-circuitpython
