# Autonomous Firefighting Robot

This repository contains the hardware documentation and source code for an autonomous firefighting robot built on an Arduino Uno architecture. The robot uses a 3-point infrared flame sensor array to detect fire sources, tracks the target using a 4-motor drivetrain, and uses a servo-steered water pump controlled via a custom-built relay switch to extinguish flames.

## Project Timeline & Build Log
* **Phase 1 (Mechanical Drivetrain):** Began construction using a custom wooden board as the main chassis base. Attached 4 BO (Battery Operated) DC gear motors to create a 4-wheel drive system. Hand-soldered the power leads to all four motors and mounted the high-traction tires. Wired the left and right motor pairs directly into the outputs of an L298N dual H-bridge motor driver.
* **Phase 2 (Sensor Mounting & Custom Brackets):** While waiting for the main microcontroller delivery, installed 3 IR flame sensors along the front lip of the chassis. Fabricated a custom raised mounting bracket out of cardboard to elevate the sensors and avoid physical interference, then mounted the SG90 micro servo motor directly on top of this platform.
* **Phase 3 (Control Integration & Power Routing):** Integrated the Arduino Uno upon delivery. Routed the main power loop from the battery holder through the L298N driver to provide a regulated 5V power rail to the Arduino. Terminated all digital logic and power lines from the flame sensors and motor driver to the microcontroller headers.
* **Phase 4 (Fluidics & Custom Relay Engineering):** Implemented a 5V mini water pump and ran flexible tubing up to the servo horn to allow left-to-right spray sweeping. Because the submersible pump lacks digital switching capabilities, engineered a custom hardware relay circuit to safely interface the Arduino's digital logic signals with the high-current analog power requirements of the pump motor.

## System Components
* **Microcontroller:** Arduino Uno
* **Chassis Platform:** Custom wood board base with a raised cardboard sensor deck
* **Drivetrain:** 4x BO DC Geared Motors + L298N H-Bridge Driver
* **Sensors:** 3x Infrared Flame Sensor Modules (Front Array)
* **Extinguishing Mechanism:** 5V Mini Submersible Water Pump + Custom Relay Switch Circuit
* **Steering Actuator:** SG90 Micro Servo Motor
* **Power Supply:** External Battery Holder Pack

## Step-by-Step Assembly Instructions

### 1. Mechanical Assembly & Drivetrain
1. Cut a wooden board to size to serve as a sturdy, low-vibration chassis base.
2. Mount the 4 BO gear motors to the four corners of the wooden base.
3. Solder insulated extension wires to the positive and negative terminals of all 4 motors.
4. Press-fit the rubber tires onto the keyed output shafts of the motors.
5. Parallel-wire the two left motors together and the two right motors together, then secure them into the OUT terminals of the L298N motor driver.

### 2. Sensor Array & Upper Deck Construction
1. Fix three IR flame sensors to the front edge of the chassis, angling them left, center, and right to establish a 180-degree detection arc.
2. Construct a small elevated platform out of cardboard over the sensor area to protect the wiring and clear up layout space.
3. Mount the SG90 micro servo motor securely on top of the cardboard platform with the output spline facing vertically upward.
4. Route a flexible water pipe from the chassis interior up to the servo horn, allowing enough slack for a clear left-to-right sweeping motion.

### 3. Electronics, Control, & Power Routing
1. Mount the Arduino Uno and the battery holder onto the wooden chassis plate.
2. Connect the battery leads to the L298N driver's power inputs, then run the 5V regulated output from the driver to the Arduino's 5V and GND pins to power the logic system.
3. Wire the digital output pins of the three flame sensors to the designated input pins on the Arduino.
4. Wire the IN1, IN2, IN3, and IN4 control pins of the L298N driver to the Arduino's digital output pins.

### 4. Custom Pump Relay Integration
1. Assemble the custom relay switching circuit to act as an isolated digital-to-analog switch for the fluidics system.
2. Connect the Arduino pump control pin to the relay signal input.
3. Wire the 5V pump's positive lead through the relay's switching contacts to the power supply rail, and ground the negative lead to the common ground system.
4. Submerge the pump inside the liquid reservoir tank and ensure the fluid line connects cleanly to the servo nozzle.

## Complete Wiring Diagram

```text
============================== POWER DISTRIBUTION ==============================
Battery Pack (+)   ---> L298N Power Input (12V Terminal)
Battery Pack (-)   ---> Common Ground Rail (GND)
L298N (5V Out)     ---> Arduino Uno (5V Pin)
L298N (GND)        ---> Arduino Uno (GND Pin)

=============================== SENSOR CHANNELS ================================
Left Flame Sensor Out   ---> Arduino Pin (Specify Pin)
Center Flame Sensor Out ---> Arduino Pin (Specify Pin)
Right Flame Sensor Out  ---> Arduino Pin (Specify Pin)
Sensors VCC (+5V)       ---> Arduino 5V Rail
Sensors GND             ---> Common Ground Rail

================================ DRIVETRAIN SYSTEM =============================
Arduino Output Pins     ---> L298N IN1, IN2, IN3, IN4 Inputs
L298N OUT1 & OUT2       ---> Left Side Motor Pair (Parallel Wired)
L298N OUT3 & OUT4       ---> Right Side Motor Pair (Parallel Wired)

============================= EXTINGUISHING SYSTEM =============================
Servo Signal (Orange)   ---> Arduino PWM Pin (Specify Pin)
Servo Power (Red)       ---> Arduino 5V Rail
Servo Ground (Brown)    ---> Common Ground Rail

Arduino Pump Signal Pin ---> Custom Relay Circuit Input
Power Supply (+)        ---> Relay Common (COM) Contact
Relay Normally Open (NO)---> 5V Water Pump Positive (+) Lead
5V Water Pump Negative ---> Common Ground Rail
```
