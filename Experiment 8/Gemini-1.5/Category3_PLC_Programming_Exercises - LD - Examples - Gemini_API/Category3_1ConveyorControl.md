## Conveyor Belt Control with 3 Stations and 5 Sensors

```
(Start of Ladder Diagram)
|                                                                                                         |
|                                                                                       +--------+       |
|                                                                                       |  TON   |       |
|    StartSensor1  StartSensor2  StartSensor3                                           |        |       |
+---| |-------+---| |-------+---| |---------------------------------------------------|IN  PT  Q|-------+
|   |         |   |         |   |                                                       |     T#2S|       |
|   +---------+   +---------+   +--------------------------------------------------------|        |       |
|                                                                                       +--------+       |
|                                                                                                         |
|                                                       +--------+                                           |
|    StopSensor1  StopSensor2  StopSensor3  StopSensor4  |  TON   |                                           |
+---| |-------+---| |-------+---| |-------+---| |-------|IN  PT  Q|-------+                                  |
|   |         |   |         |   |         |   |       |     T#2S|       |                                  | 
|   +---------+   +---------+   +---------+   +-------|        |       |                                  |
|                                                       +--------+                                           |
|                                                                                                         |
|                                                                      +--------+                            |
|                                                                      |  CTU   |                            |
|                                   Station1Stop  Station2Stop  Station3Stop|        |                            |
+-----------------------------------| |-------+---| |-------+---| |-------|CU  PV  Q|-------( )---------------+
|                                   |         |   |         |   |       |     0   0 | ConveyorMotor            | 
|                                   +---------+   +---------+   +-------|        | (Speed = 2 m/s)         | 
|                                                                      +--------+                            | 
|                                                                                                         |
|               +-----------------------------------------------+                                           |
|               |                                               |                                           |
|    AnyStop   -| OR                                             |-------------------------------------------|
|               |                                               |                                           |
|               +-----------------------------------------------+                                           |
|                                                                                                         |
(End of Ladder Diagram)
```

**Explanation:**

1. **Start Sensors:** The conveyor starts when any of the three start sensors (StartSensor1, StartSensor2, StartSensor3) detect an object. Each sensor triggers a TON (Timer On Delay) with a 2-second delay to avoid immediate stops due to transient object presence.

2. **Stop Sensors:** The conveyor stops when any of the four stop sensors (StopSensor1, StopSensor2, StopSensor3, StopSensor4) detect an object. Similar to the start sensors, each stop sensor triggers a TON with a 2-second delay.

3. **Station Stops:**  Three normally open contacts represent stop buttons at each station (Station1Stop, Station2Stop, Station3Stop). Pressing any of these buttons will stop the conveyor.

4. **Conveyor Motor Control:** 
    * A CTU (Count Up) instruction with a preset value of 0 is used to ensure the motor starts and stops cleanly. 
    * The output of the CTU (Q) controls the ConveyorMotor. 
    * The CTU is incremented when any of the start sensors' TON timers are active and decremented when any of the stop sensors' TON timers are active or any station stop button is pressed. 
    * This logic ensures the motor only runs when there's a continuous flow of objects and stops when there's a blockage, a stop signal from a sensor, or a manual stop from any station.

5. **Any Stop Condition:**  An OR block combines all stop conditions (stop sensors' TON outputs and station stop buttons) to create a single "AnyStop" signal that feeds into the CTU's decrement (CU) input. 

**Additional Notes:**

* This program assumes the sensors and buttons are already configured and connected to the PLC inputs.
* The ConveyorMotor output should be connected to the appropriate motor control circuit.
* You might need to adjust the TON timer presets depending on the conveyor belt's length and desired responsiveness. 
* Consider adding safety measures, such as emergency stop buttons and safety relays, for a complete system. 
