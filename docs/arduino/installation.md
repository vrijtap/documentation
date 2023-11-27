# Arduino Installation

In this project, the Arduino controlls the servo's, weight sensor and pump. The required installation will be described here.

## Fetching the Git Project

The following commands are ran in Git Bash:

```bash
mkdir ~/Git && cd ~/Git
git clone -b main https://github.com/vrijtap/arduino-uno.git
```

The Git repository should now be located in C:\Users\User\Git

## General Arduino

To install the Arduino, you'll have to download the installation online. After installing the environment, you should follow the circuit documentation to create the circuits required to make this project work. After that, you can plug the arduino into your laptop and the Arduino IDE will automatically detect the USB port associated with an Arduino connected to it.

## Uploading Project

Under 'files', select 'open'. Find the 'arduino-uno/' folder on your machine that you've cloned with Git and open 'arduino-uno.ino'. Finally click on the publish button in the Arduino IDE after selecting the COM port associated with 'Arduino Uno'.
