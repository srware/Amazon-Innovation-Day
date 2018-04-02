# Setting Up The Up Squared Board
The Up Squared Grove IoT Developer Kit includes the following components:

 - Up Squared Board + Power Supply
 - GrovePi Shield
 - Grove Sensors
	 - LCD Screen
	 - Rotary Angle Sensor
	 - Light Sensor
	 - Temperature & Humidity Sensor
	 - Button
	 - LED
 - Micro USB Cable
 - USB Stick

## Connections
There are 2 ways of communicating with the board out-of-the-box:

 1. Serial (via USB cable)
 2. HDMI Monitor + Keyboard

Follow these [instructions](https://software.intel.com/en-us/upsquared-grove-getting-started-guide-power-on-board) to connect the board. You can substitute the Serial USB connection for a HDMI monitor and USB keyboard if preferred.

### Serial Connection
To communicate via serial use your favourite serial console application such as **screen** or **Putty** with a baud rate of **115200**. In Linux the serial device will show up as **/dev/ttyACM***. Below is an example for connecting to the board from **Linux** using **Screen**:
``` bash
sudo screen /dev/ttyACM0 115200
```
> **NOTE:** You may need to hit **Enter** a few times after a connection is established to start getting output in the console window.
## OS
The Up Squared board comes pre-installed with Ubuntu Server 16.04.

### Default Login
 - Username: **upsquared**
 - Password: **upsquared**

### Graphical Desktop
If you require a graphical desktop you can install the default Ubuntu desktop with the following command:
``` bash
sudo apt install ubuntu-desktop
sudo reboot
```
The board will now reboot into the graphical desktop by default.

