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


## RFIDLib

The Rfid library enables the device to use the rfid-rc522 device. It uses the modules RPi.GPIO and mfrc522.

---

### `readerRFID.Rfid()`

**Description:**
Creates an instance of the rfid class.

**Example:**

```py
    from rfidLib import readerRFID
    rfid = readerRFID.Rfid()

```
---

### `rfid.write(data)`

**Description:**
The rfid_write function will write the given data to an rfid writable object, eg. myfairclassic cards. This function is only to write without much checks being in place. It will give an exception if the write process has failed.

**Parameters:**

- `data`: This can be anything, preferably a string.

**Example:**

```py
    rfid.write(string_of_words)
```
### `rfid.read()`

**Description:**
The read function will enable the rfid module to read data from any carrying rfid object in range of the reader. It will read what has been written to the medium and it will perform a check to see if it is the correct size of 48. This size is chosen based upon the lenght of the MongoDB ID size.
---
This  function will return the read data.

**Example:**

```py
    data_on_card = rfid.read()
```

### `rfid.closeGPIO()`

**Description:**
This function has to be called at the end of the whole program to reset the GPIO usage on the RaspberryPi.

**Example:**

```py
    # End of program, shutting down.
    rfid.closeGPIO() 
```
---


## MongoLib

The mongo library enables the device to use the mongodb functions in a simple fashion. It uses the modules pymongo, bson, pymongo.errors and bson.errors.

---

### `mdb = mongo.Mongo(uri, database_name, collection_name)`

**Description:**
Creates an instance of the mongo library class. Will connect to a mongo database using the variables given. 
The function will also give an exception if setting up the connection takes longer than 30 seconds.

**Parameters:**

- `uri`: This should be a URI value to connect to a database.
- `database_name`: This should be the name of the database.
- `collection_name`: This should be the name of the collection.

**Example:**

```py
    from mongoLib  import mongo
    mdb = mongo.Mongo(uri, 'backend', 'cards')
```
---

### `mdb.userExists(uid: str)`

**Description:**
The userExists function will look in the database if there is a user with the ID supplied to the function. It will return a True or False based upon the results found. If the user exists this function will also aquire the data about how many drinks there are left for this user.

---
If there is an invalid user ID supplied to the function it will return a False and notify that the type of data is the wrong format.

**Parameters:**

- `uid`: The ID of the user you are trying to find. This must be a string.

**Example:**

```py
    if mdb.userExists(uid) == True: 
        # Do something
```
### `mdb.decreaseBeer()`

**Description:**
This function will check if the user still has their "beers" value in the positives. If not, there wont be a reduction in this value on the database. If there is a positive balance, there will be an increase of -1 to the database value "beers".
---
This  function will return False if a wrong uid is given to the mdb.userExists(uid) function.

**Example:**

```py
    mdb.decreaseBeer()
```

### `mdb.closeConnection()`

**Description:**
This function will close the database connection.

**Example:**

```py
    # End of program, shutting down.
    mdb.closeConnection() 
```
---