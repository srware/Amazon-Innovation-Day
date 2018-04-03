# Sensors
The Up Squared Grove IoT Developer Kit includes a selection of sensors. Below is some sample code for communicating with these sensors using the included **GrovePi** shield.

## Overview
To interface with low-level IO on the Up Squared board we will use a library called [MRAA](https://github.com/intel-iot-devkit/mraa). To interface with specific sensors at a high-level we will use the [UPM](https://github.com/intel-iot-devkit/upm) library which offers support for [400+ sensors](https://upm.mraa.io/findSensor.html).

To interface with the IO on the GrovePi shield you are required to use the **Subplatform API** in **MRAA**. This means you need to add an offset of **512** to any IO calls. So **D4** would become **516 (512 + 4)** and **A1** would become **513 (512 + 1)**. See the documentation linked below for more information.

The Up Squared also has native IO which is pin compatible with the Raspberry Pi IO header. This can also be accessed using the **MRAA** library.

#### Documentation
[GrovePi Shield MRAA Documentation](https://github.com/intel-iot-devkit/mraa/blob/master/docs/grovepi.md)
[Up Squared Native IO MRAA Documentation](https://github.com/intel-iot-devkit/mraa/blob/master/docs/up2.md)

> **Note:** The default **upsquared** user does not have the required privileges to access low-level devices. As such whenever you run code which is accessing a sensor using **MRAA** or **UPM** always run with elevated privileges.

