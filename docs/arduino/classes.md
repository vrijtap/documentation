# Arduino Classes

In this file, all of the classes made for the Arduino are discribed in terms of how to initialize them and use them.

## High Torque Servo

The High Torque Servo is a servo meant for heavy loads. The Servo is powerful with the drawback of it consuming more power. The following functions can be used in our project to utilize it:

---

### `HighTorqueServo(int minAngle, int maxAngle)`

**Description:**
Creates an instance of the High Torque Servo class with specified angle limits.

**Parameters:**

- `minAngle`: Minimum angle limit (accepted range: [0, 180]).
- `maxAngle`: Maximum angle limit (accepted range: [0, 180]).

**Example:**

```cpp
#include "HighTorqueServo.h"

// Initialize a High Torque Servo with angle limits
HighTorqueServo myHighTorqueServo(0, 180);
```

---

### `void init(uint8_t servoPin, float percentage)`

**Description:**
Initialize the High Torque Servo. This function needs to be called in the setup function within the Arduino .ino file.

**Parameters:**

- `servoPin`: Pin number for the servo.
- `percentage`: Initial percentage turned (accepted range: [0.0, 100.0]).

**Example:**

```cpp
void setup() {
    myHighTorqueServo.init(6, 0.0);
}
```

---

### `void write(float percentage)`

**Description:**
Turns the servo into a position based on the percentage of the minimum and maximum angle.

**Parameters:**

- `percentage`: Percentage to turn to (accepted range: [0.0, 100.0]).

**Example:**

```cpp
#include <Arduino.h>

void loop() {
    delay(1000);
    myHighTorqueServo.write(100.0);
}
```

---

After performing all of the functions in the documentation you will succesfully initialize the servo with a resricted minimum and maximum angle and you will have moved it from 0 percent of that angle to 100 percent. This results in the Servo moving from 0 degrees to 180 degrees.
