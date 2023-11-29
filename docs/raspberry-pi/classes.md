# RaspberryPi Classes

In this file, all of the classes made for the RaspberryPi 4B+ are generally discribed in their use and initialisation.

**Disclaimer:** Once the libraries have been initialized you can use the functions included within them.

## cameraLib

The camera library enables the camera by using the picam2 module.

---

### `camera.Camera(picture_size)`

**Description:**
Creates an instance of the camera class with specified size.

**Parameters:**

- `picture_size`: The height and width size of the picture (accepted value: [64]).

**Example:**

```py
    from cameraLib  import camera
    cam = camera.Camera(64)
```
---

### `cam.burst(path, name, amount, seconds)`

**Description:**
The burst function creates a set of images seperated by a given time. The images will be saved as .jpg.

**Parameters:**

- `path`: The location where the images should be saved at.
- `name`: The name of the images. Is set per image and will be wrapped by datatime data.
- `amount`: The amount of pictures to be taken.
- `seconds`: The timing in between pictures being taken.

**Example:**

```py
    cam.burst("~/path_to_image_folder", "image_name", 30, 1)
```

---

### `cam.capture(path, name)`

**Description:**
The capture function creates a single image and saves it, as a .jpg, to a given location.

**Parameters:**

- `path`: The location where the images should be saved at.
- `name`: The name of the images. Is set per image. Is set per image and will be wrapped by datatime data.

**Example:**

```py
    cam.capture("~/path_to_image_folder", "image_name")
```

---
### `cam.captureArray()`

**Description:**
The captureArray function creates an array wherein the imagedata is saved. It will return this array.

**Example:**

```py
    image_array = cam.captureArray()
```

---

## i2cLib

The I2C library enables the device to use the I2C communication channel in a simple fashion. It uses the smbus2 module.

---

### `bus.Bus(port, adress)`

**Description:**
Creates an instance of the i2c class with specified adress and port.

**Parameters:**

- `port`: The port the I2C connection is set up from (Default: [1]).
- `adress`: The height and width size of the picture (Default: [0x8]).

**Example:**

```py
    from i2cLib import bus
    i2c = bus.Bus(1, 0x8)

```
---

### `bus.send_data(data)`

**Description:**
The send_data function will send out the handed data. Given that it is an integer and within one byte.

**Parameters:**

- `data`: This can be any int value as long as it is in one byte. Otherwise it will restart again from 0. (Recommended range: [0, 255]).

**Example:**

```py
    i2c.send_data(32)
```
### `bus.receive_data()`

**Description:**
The receive_data function will poll the slave for any changes on the I2C bus. it will receive what the value on the slave currently is.

**Example:**

```py
    polled_message = i2c.receive_data()
```
### `bus.send_and_check(data)`

**Description:**
The send_and_check function will send out a message to the slave and requires the slave to echo the same message back, this is done to know for sure the message has been delivered to the slave. 

This function also returns a True or False depending on if the message was delivered succesfully.

**Parameters:**

- `data`: This can be any int value as long as it is in one byte. Otherwise it will restart again from 0. (Recommended range: [0, 255]).

**Example:**

```py
    if i2c.send_and_check(1):
        #do something here
```
---
