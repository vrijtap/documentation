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

To enable the camera on the RaspberryPi you will need to turn the legacy camera on in the config screen, you can do this by running the command:
```bash
sudo raspi-config
```

Here you should select the Interface options and turn on the legacy camera support. After this you can close this screen and reboot the pi.


Next up you should edit the config.txt and you should add two lines to make the camera detectable. 

```bash
sudo nano /boot/config.txt

#Add two lines to the end of the file
dtoverlay=imx219
camera_auto_detect=0
```

