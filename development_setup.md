# Development Setup
The Up Squared board comes pre-installed with Ubuntu Server 16.04 which means you are free to install your favourite Linux-based code editor, IDE, runtimes etc... Below we will focus on 3 options, **Arduino(R) Create**, **Python** and **Node.js**.

## Arduino(R) Create
[Arduino(R) Create](https://create.arduino.cc/) is a cloud-based IDE which now has support for Intel(R) IoT platforms such as the Up Squared board. There is a comprehensive "Getting Started Guide" available [HERE](https://software.intel.com/en-us/upsquared-grove-getting-started-guide).

The Arduino(R) Create IDE includes a number of example projects to quickly get you up and running communicating with sensors etc...

## Python
The Ubuntu Server image come with Python already installed. If you want to work with the **Grove Sensors** using the **MRAA** and **UPM** libraries (recommended) run the following command:
``` bash
sudo apt install python-mraa python-upm
```
## Node.js
To install Node.js support run the following command:
``` bash
sudo apt install nodejs nodejs-legacy
```
