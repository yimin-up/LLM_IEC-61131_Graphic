```
(Start of Sequential Function Chart)

        +----------------------<------------------------+
        |                                               |
        |                                               |
+============+                                          |
||          ||                                          |
|| Initial  ||                                          |
||          ||                                          |
+============+                                          |
        |                                               |
        |                                               |
        + (Temp < 20)                                     |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|     HeatOn     |   |  N   |  HeaterOn  |        |      |
|               |---|      |            |        |      |
|               |   |      |            |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + (Temp > 22)                                     |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|    HeatOff    |   |  N   | HeaterOff   |        |      |
|               |---|      |            |        |      |
|               |   |      |            |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        +----------------------->-----------------------+

(End of Sequential Function Chart)
```
**Explanation:**

*   **Initial Step:** The program starts in the "Initial" step.
*   **Heating On:** If the temperature (Temp) falls below 20 degrees Celsius, the transition to the "HeatOn" step is triggered. This activates the "HeaterOn" output, turning on the heating system. 
*   **Heating Off:** If the temperature rises above 22 degrees Celsius, the transition to the "HeatOff" step is triggered. This activates the "HeaterOff" output, turning off the heating system.
*   **Continuous Regulation:** The program continuously monitors the temperature and cycles between the "HeatOn" and "HeatOff" steps as needed to maintain the temperature within the desired range. 

**Additional Considerations:**

*   **Sensor Input:** The program assumes the existence of a temperature sensor that provides the "Temp" input variable. 
*   **Heater Control:** The "HeaterOn" and "HeaterOff" outputs should be connected to the control circuit of the heating system.
*   **Hysteresis:** The use of a temperature range (20-22 degrees Celsius) with a slight difference between the turn-on and turn-off points introduces hysteresis, which helps prevent rapid cycling of the heating system.
*   **Safety:** Depending on the specific heating system and application, additional safety measures and interlocks may be necessary. 
