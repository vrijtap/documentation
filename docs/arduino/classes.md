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

## StateMachine

### Overview

The `StateMachine` class implements a state machine that manages transitions between `SM_IDLE_STATE`, `SM_TAPPING_STATE`, and `SM_PAUSED_STATE` based on specific events: `SM_ZERO` and `SM_ONE`.

#### Constants

- `SM_IDLE_STATE`: Represents the idle state (value: 0).
- `SM_TAPPING_STATE`: Represents the tapping state (value: 1).
- `SM_PAUSED_STATE`: Represents the paused state (value: 2).
- `SM_ZERO`: Represents event zero.
- `SM_ONE`: Represents event one.

### Class Members

#### Constructor

##### `StateMachine()`

Creates an instance of the `StateMachine` class with an initial state of `SM_IDLE_STATE`.

#### Methods

##### `void handleInputEvent(int SM_event)`

Handles input events and manages state transitions.

- `SM_event`: The event triggering the state transition (`SM_ZERO` or `SM_ONE`).

##### `int getState() const`

Gets the current state of the StateMachine.

- Returns: `int` - The current state of the StateMachine.

### Usage Example

```cpp
#include "StateMachine.h"

// Create a StateMachine instance
StateMachine stateMachine;

void setup() {
    stateMachine.handleInputEvent(SM_ONE); // Perform state transitions based on events
}

void loop() {
    int currentState = stateMachine.getState(); // Get the current state
    // Perform actions based on currentState
}
```

## Loadcell

### Overview

The arduino will make use of a loadcell to determine the percentage of liquids left in the tank. 


### `HighTorqueServo(int minAngle, int maxAngle)`

**Description:**
Creates an instance of the High Torque Servo class with specified angle limits.

**Parameters:**

- `doutPin`: pin used for digital output (desired: Digital pin 2).
- `sckPin`: pin used for sck (desired: Digital pin 3).

**Example:**

```cpp
#include "Scale.h"  

// Constructor: Initializes the Scale object with specified pins and calibration factor
Scale::Scale(int doutPin, int sckPin)
  : doutPin(doutPin), sckPin(sckPin) {
}
```
---
#### Methods

##### `void Scale::init()`

Sets up the scale and runs the reset function once to calibrate the scale to 0. The scale factor is also applied here.

##### `void Scale::reset()`

Uses the built in tare function to recalibrate the scale to 0.


##### `float Scale::getWeight()`

Returns the current weight of the tank in grams.

- Returns: `float` - The current weight of the tank.


##### `int Scale::getPercentage()`

Returns the current percentage of liquids in the tank.

- Returns: `int` - The current percentage.

### Usage Example

```cpp
#include "Scale.h"
#include <Wire.h>

const int LOADCELL_DOUT_PIN = 2;  
const int LOADCELL_SCK_PIN = 3;   

// Create a scale instance
Scale scale(LOADCELL_DOUT_PIN, LOADCELL_SCK_PIN);


void setup() {
  scale.init(); // initializes the scale
}

void loop() {
    int currentState = stateMachine.getState(); // Get the current state
    int percentage = scale.getPercentage(); // Get the percentage of the tank.
}
```


