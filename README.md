
# FireFighting Robot

A simple Arduino-based robot that detects open flames, drives toward them, and puts them out using a mini water pump and a sweeping servo motor.

## Component List
*  Arduino Uno
*  3x Flame Sensor modules (Left, Center, Right)
*  L298N Motor Driver + DC Gear Motors
* 5V Mini Submersible Water Pump + SG90 Micro Servo (to spray water back and forth)
* 2x 18650 Li-ion batteries


*(Note: If you downloaded an image of your diagram, you can add this line instead: You can find the uploaded schematic file (`circuit.png`) right here in the main folder of this repository.)*

## Pin Layout
* **Flame Sensors:** Connected to pins (Left, Center, Right) to track where the fire is.
* **Motor Driver:** Linked to PWM pins to drive the wheels forward or turn toward the flame.
* **Servo & Pump:** Connected to digital output pins to trigger the spraying mechanism once the robot gets close enough to the fire.

## How it Works
The code runs an active loop checking all three flame sensors. If the left or right sensor spots a flame, the robot rotates in that direction. Once the center sensor detects that the fire is directly ahead, it drives forward. When it gets close enough, the wheels stop, the servo starts panning the nozzle back and forth, and the water pump switches on until the fire is cleared.
