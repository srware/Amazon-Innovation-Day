# Sensors
The Up Squared Grove IoT Developer Kit includes a selection of sensors. Below is some sample code for communicating with these sensors using the included **GrovePi** shield.

## Overview
To interface with low-level IO on the Up Squared board we will use a library called [MRAA](https://github.com/intel-iot-devkit/mraa). To interface with specific sensors at a high-level we will use the [UPM](https://github.com/intel-iot-devkit/upm) library which offers support for [400+ sensors](https://upm.mraa.io/findSensor.html).

To interface with the IO on the GrovePi shield you are required to use the **Subplatform API** in **MRAA**. This means you need to add an offset of **512** to any IO calls. So **D4** would become **516 (512 + 4)** and **A1** would become **513 (512 + 1)**. See the documentation linked below for more information.

The Up Squared also has native IO which is pin compatible with the Raspberry Pi IO header. This can also be accessed using the **MRAA** library.

### Documentation

 - [GrovePi Shield MRAA Documentation](https://github.com/intel-iot-devkit/mraa/blob/master/docs/grovepi.md)
 - [Up Squared Native IO MRAA Documentation](https://github.com/intel-iot-devkit/mraa/blob/master/docs/up2.md)

> **Note:** The default **upsquared** user does not have the required privileges to access low-level devices. As such whenever you run code which is accessing a sensor using **MRAA** or **UPM** always run with elevated privileges.

## Sample Code
### Grove LCD RGB Backlight
The LCD screen and RGB backlight is an **I2C** device so needs to be connected to one of the **I2C** connectors on the **GrovePi** shield (e.g. **I2C-2**).
#### Python
``` python
from upm import pyupm_jhd1313m1 as lcd

# Initialise JHD1313 at 0x3E (LCD_ADDRESS) and 0x62 (RGB_ADDRESS)
myLcd = lcd.Jhd1313m1(0, 0x3E, 0x62)

# RGB Red
myLcd.setColor(255, 0, 0)

myLcd.setCursor(0,0)
myLcd.write('Hello World')
myLcd.setCursor(1,2)
myLcd.write('Hello World')
```
#### Node.js

### Rotary Angle Sensor
The Rotary Angle Sensor is an **analog** device so needs to be connected to one of the **analog** inputs on the **GrovePi** shield (e.g. **A0**).
#### Python
``` python
import mraa
from upm import pyupm_grove as grove

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# New rotary sensor on AIO pin 0
rotary = grove.GroveRotary(512)

# Read absolute values
abs = rotary.abs_value()
absdeg = rotary.abs_deg()
absrad = rotary.abs_rad()

# Read relative values
rel = rotary.rel_value()
reldeg = rotary.rel_deg()
relrad = rotary.rel_rad()

print("Absolute values | Raw: %4d" % int(abs), " Degrees: %3d" % int(absdeg), " Radian: %5.2f" % absrad)
print("Relative values | Raw: %4d" % int(rel) , " Degrees: %3d" % int(reldeg), " Radian: %5.2f" % relrad)
```
#### Node.js
