# Raspberry Pi Installation

Due to the Raspberry Pi being an operating system running the server, AI and a couple of sensors, there is a bunch of installations to be done before the pi can operate within the project. The operating system you need to install is a 64-bit headless raspbian installation with access to your wireless network and an open SSH port.

## Git Installation on a fresh Pi

Ofcourse we need to install Git, as our project is based on Github.

Clone the project

```bash
sudo apt update
sudo apt upgrade
sudo apt install git
git clone https://github.com/vrijtap/raspberry-pi.git
cd raspberry-pi
ls
```


## Camera Installation

To enable the camera on the RaspberryPi you will need the 

