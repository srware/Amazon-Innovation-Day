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
``` js
// Load LCD module on I2C
var LCD = require('jsupm_jhd1313m1');

# Initialise JHD1313 at 0x3E (LCD_ADDRESS) and 0x62 (RGB_ADDRESS)
var myLcd = new LCD.Jhd1313m1 (0, 0x3E, 0x62);

// RGB Red
myLcd.setColor(255, 0, 0);

myLcd.setCursor(0,0);
myLcd.write('Hello World');
myLcd.setCursor(1,2);
myLcd.write('Hello World');
```

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
``` js
const mraa = require('mraa');
const grove = require('jsupm_grove');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0");

// New rotary sensor on AIO pin 0
var groveRotary = new grove.GroveRotary(512);

var abs = groveRotary.abs_value();
var absdeg = groveRotary.abs_deg();
var absrad = groveRotary.abs_rad();

var rel = groveRotary.rel_value();
var reldeg = groveRotary.rel_deg();
var relrad = groveRotary.rel_rad();


console.log("Absolute: " + abs + " " + Math.round(parseInt(absdeg)) + " " + absrad.toFixed(3));
console.log("Relative: " + rel + " " + Math.round(parseInt(reldeg)) + " " + relrad.toFixed(3));
```

### Grove Light Sensor
The Grove Light Sensor is an **analog** device so needs to be connected to one of the **analog** inputs on the **GrovePi** shield (e.g. **A0**).
#### Python
``` python
import mraa
from upm import pyupm_grove as grove

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# Create a light sensor object using AIO pin 0
light = grove.GroveLight(512)

raw = light.raw_value()
lux = light.value();

print("Raw value is %d" % raw + ", which is roughly %d" % lux + " lux");
```
#### Node.js
``` js
const mraa = require('mraa');
const grove = require('jsupm_grove');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0");

// Create the light sensor object using AIO pin 0
var light = new grove.GroveLight(512);

var raw = light.raw_value();
var lux = light.value();

console.log("Raw value is " + raw + ", which is roughly " + lux + " lux");
```

### LED
The LED socket is a **digital** actuator so needs to be connected to one of the **digital** inputs on the **GrovePi** shield (e.g. **D4**).
#### Python
``` python
import time
import mraa
from upm import pyupm_led

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# Create the Grove LED object using GPIO pin 4 (D4)
led = pyupm_led.Led(516)

# Turn the LED on and off 10 times, pausing one second between transitions
for i in range (0,10):
    led.on()
    time.sleep(1)
    led.off()
    time.sleep(1)
```
#### Node.js
``` js
const mraa = require('mraa');
const ledSensor = require('jsupm_led');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0");

// Create the LED object using GPIO pin 4 (D4)
var led = new ledSensor.Led(516);

// Turn the LED on and off 10 times, pausing one second between transitions
var i = 0;
var waiting = setInterval(function() {
    if ( i % 2 == 0 ) {
        led.on();
    } else {
        led.off();
    }

    i++;
    
    if ( i == 20 ) clearInterval(waiting);
    
}, 1000);
```

### Button
The Button is a **digital** actuator so needs to be connected to one of the **digital** inputs on the **GrovePi** shield (e.g. **D4**).
#### Python
``` python
import time
import mraa
from upm import pyupm_grove as grove

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# Create the button object using GPIO pin 4 (D4)
button = grove.GroveButton(516)

# Read the input and print, waiting one second between readings
while 1:
    print(button.name(), ' value is ', button.value())
    time.sleep(1)
```
#### Node.js
``` js
const mraa = require('mraa');
var upm = require('jsupm_button');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0");

// Create the button object using GPIO pin 4 (D4)
var button = new upm.Button(516);

// Read the input and print, waiting one second between readings
function readButtonValue() {
    console.log(button.name() + " value is " + button.value());
}

setInterval(readButtonValue, 1000);
```


### Button
The Button is a **digital** actuator so needs to be connected to one of the **digital** inputs on the **GrovePi** shield (e.g. **D4**).
#### Python
``` python
import time
import mraa
from upm import pyupm_grove as grove

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# Create the button object using GPIO pin 4 (D4)
button = grove.GroveButton(516)

# Read the input and print, waiting one second between readings
while 1:
    print(button.name(), ' value is ', button.value())
    time.sleep(1)
```
#### Node.js
``` js
const mraa = require('mraa');
var upm = require('jsupm_button');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0");

// Create the button object using GPIO pin 4 (D4)
var button = new upm.Button(516);

// Read the input and print, waiting one second between readings
function readButtonValue() {
    console.log(button.name() + " value is " + button.value());
}

setInterval(readButtonValue, 1000);
```

### Temperature & Humidity Sensor
The Temperature & Humidity sensor is an **I2C** sensor so needs to be connected to one of the **I2C** inputs on the **GrovePi** shield (e.g. **I2C-1**).
#### Python
``` python
import mraa
from upm import pyupm_si7005 as upm

# Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

# Initialise sensor
sensor = upm.SI7005(0, 512)

temp = sensor.getTemperatureCelsius()
hum = sensor.getHumidityRelative()

print("Temperature is currently %d" % temp + " C");
print("Humidity is currently %d" % hum + " %");
```
#### Node.js
``` js
const mraa = require('mraa');
const upm = require('jsupm_si7005');

// Initialise GrovePi subplatform
mraa.addSubplatform(mraa.GROVEPI, "0")

// Initialise sensor
var sensor = new upm.SI7005(0, 512)

var temp = sensor.getTemperatureCelsius()
var hum = sensor.getHumidityRelative()

console.log("Temperature is currently " + temp + " C");
console.log("Humidity is currently " + hum + " %");
```
