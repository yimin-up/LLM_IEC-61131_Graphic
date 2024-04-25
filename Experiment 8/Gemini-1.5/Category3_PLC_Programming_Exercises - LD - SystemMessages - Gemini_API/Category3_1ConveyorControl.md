## Conveyor Belt Control with 3 Stop Stations

```
--| |------------------------------------------------------------------------( )--
  |                                                                            |
  |--[SENSOR 1]-------------------------------------[ ]-----------------------|
  |                                                |
  |--[SENSOR 2]-------------------------------------|
  |                                                |
  |--[SENSOR 3]-------------------------------------|
  |                                                |
  |--[SENSOR 4]-------------------------------------|-------[STOP STATION 1]--|
  |                                                                            |
  |--[SENSOR 5]----------[STOP STATION 2]----------[STOP STATION 3]----------|
  |                                                                            |
--| |--------------------------------( )--------------------------------------|--
  |                                   |
  |--( )-------[MOTOR]------------------|    Speed Control (2 m/s)
  |
  |
  |--[START/STOP]-----------------------|
```

**Explanation:**

*   **Sensors:** The system uses five sensors (SENSOR 1 to SENSOR 5) to detect the presence of objects on the conveyor belt. 
*   **Stop Stations:** There are three stop stations where users can manually stop the conveyor belt. Each stop station is represented by a normally closed contact, which opens when the stop button is pressed.
*   **Motor Control:** The motor is controlled by a normally open contact in series with all the sensor contacts and stop station contacts. This ensures the motor only runs when:
    *   There is an object on the conveyor belt (at least one sensor is activated)
    *   No stop button is pressed
*   **Start/Stop Button:**  A start/stop button provides manual control over the entire system.
*   **Speed Control:** The speed control is assumed to be handled separately and is set to maintain a constant speed of 2 meters per second.

**Logic:**

1.  The conveyor belt starts when:
    *   The START/STOP button is pressed (assuming it is a maintained switch)
    *   At least one sensor detects an object
    *   No stop button at any station is pressed
2.  The conveyor belt stops when:
    *   The START/STOP button is pressed again
    *   No sensors detect an object 
    *   Any stop button at any station is pressed 

**Note:** This is a basic representation of the conveyor belt system. Additional features such as emergency stops, motor overload protection, and more complex sensor logic can be added based on specific requirements.
