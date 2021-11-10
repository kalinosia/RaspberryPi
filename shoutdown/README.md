
## Hardware

![](https://www.quartoknows.com/uploads/pics/Raspberry-Pi-Projects/Shutdown-Button/thumbs/495x495Shutdown-Button-MAIN.jpg)

##### You need:
- Raspberry Pi
- Button
- Connecting cables female-male
- Breadboard


![](https://www.quartoknows.com/uploads/pics/Raspberry-Pi-Projects/Shutdown-Button/thumbs/400x400SIMPLE-SHUTDOWN-1DETAIL.png)

You'll need to select a GPIO. Here we are interested in using one of the pins to detect a button press: the button will be connected between the GPIO pin and the ground pin, so pressing the button reduces the voltage to zero.
For this project, select GPIO 21, which is at one end of the connector, right next to the ground pin (you are free to use any other unused GPIO).

![](https://www.quartoknows.com/uploads/pics/Raspberry-Pi-Projects/Shutdown-Button/thumbs/287x292SIMPLE-SHUTDOWN-2DETAIL.png)


## Code
```
# !/bin/python

import RPi.GPIO as GPIO

import time

import os

 

# Use the Broadcom SOC Pin numbers

# Setup the pin with internal pullups enabled and pin in reading mode.

GPIO.setmode(GPIO.BCM)

GPIO.setup(21, GPIO.IN, pull_up_down=GPIO.PUD_UP)

 

# Our function on what to do when the button is pressed

def Shutdown(channel):

    print("Shutting Down")

    time.sleep(3)

    os.system("sudo shutdown -h now")

 

# Add our function to execute when the button pressed event happens

GPIO.add_event_detect(21, GPIO.FALLING, callback=Shutdown, bouncetime=2000)

 

# Now wait!

while 1:

    time.sleep(1)
```


### Alternative
```
from subprocess import call

#code..
call("sudo nohup shutdown -h now", shell=True)
```

## Source
https://www2.quartoknows.com/page/raspberry-pi-shutdown-button
