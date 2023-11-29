# RaspberryPi Classes

In this file, all of the classes made for the RaspberryPi 4B+ are generally discribed in their use and initialisation.

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
**Disclaimer:** Once the library has been initialized you can use the functions included within it, these are listed below.
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
