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

## RFID Module Installation

To enable the RFID-RC522 module you will need to connect it to the RaspberryPi as shown in the images in the Circuit page.

Now you can boot up the RaspberryPi and go to the configuration screen.

```bash
sudo raspi-config
```

Here you should enable the SPI setting in Interface options and reboot the Pi.

Now the Pi has enabled the SPI inteface and now you can install spidev and the module needed for the RFID module:

```bash
sudo pip3 install --upgrade spidev
sudo pip3 install mfrc522
```

Now the Pi should be able to use the RFID library functions.

## I2C Module Installation

To enable the I2C functions you should again head to the configuration screen:

```bash
sudo raspi-config
```

Head to the interface options and enable I2C there. After this you should reboot the Pi.

After booting the pi up again you should install the smbus2 packages to make the I2C library function.

```bash
pip install smbus2
```

## MongoDB Package Installation

To use the functions in the mongo library included in the project you should install some packages for it to work.

```bash
python3 -m pip install pymongo
pip install bson
```

After installing these packages you should be able to use the functions in the Mongo Library.