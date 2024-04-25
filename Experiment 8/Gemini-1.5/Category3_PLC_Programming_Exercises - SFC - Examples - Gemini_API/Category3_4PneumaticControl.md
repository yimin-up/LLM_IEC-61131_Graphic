## Pneumatic System Control with SFC

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
        + NOT Actuator_Signal                          | 
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|     Idle     |   |  N   | Compressor_Off |        |      |
|               |   |      | Valve_Closed   |        |      |
|               |   |      | Flow_Setpoint := 0 |   |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + Actuator_Signal                             |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  Start_Flow   |   |  N   | Compressor_On  |        |      |
|               |   |      | Valve_Open     |        |      |
|               |   |      | Flow_Setpoint := 50 |   |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + Pressure < 5.5                             |
        |                                               |
        |                                               |
+---------------+                                       |
| Pressure_Low  |                                       |
|               |                                       |
|               |                                       |
+---------------+                                       |
        |                                               |
        |                                               |
        + Pressure > 6.0                             |
        |                                               |
        |                                               |
+---------------+                                       |
|Pressure_High   |                                       |
|               |                                       |
|               |                                       |
+---------------+                                       |
        |                                               |
        |                                               |
        +----------------------->-----------------------+

(End of Sequential Function Chart)
```

**Explanation:**

1. **Initial Step:** The system starts in the "Initial" step. 
2. **Idle State:** If there is no signal from the actuator (`NOT Actuator_Signal`), the system transitions to the "Idle" step. Here, the compressor is turned off (`Compressor_Off`), the valve is closed (`Valve_Closed`), and the flow setpoint is set to 0. 
3. **Start Flow:** When the actuator signal is received (`Actuator_Signal`), the system moves to the "Start_Flow" step. This activates the compressor (`Compressor_On`), opens the valve (`Valve_Open`), and sets the desired flow rate to 50 standard liters per minute (`Flow_Setpoint := 50`).
4. **Pressure Monitoring:** The system continuously monitors the pressure. If the pressure falls below 5.5 bar (`Pressure < 5.5`), it enters the "Pressure_Low" state. If the pressure exceeds 6.0 bar (`Pressure > 6.0`), it enters the "Pressure_High" state.
5. **Pressure_Low and Pressure_High States:** These states can be used to trigger alarms or implement additional control logic to adjust the compressor or valve settings and bring the pressure back within the desired range. 

**Additional Considerations:**

* This SFC program is a basic framework and can be extended with additional functionality, such as:
    * **Safety interlocks:** To shut down the system in case of emergencies.
    * **Flow control:** To adjust the flow rate based on actual demand.
    * **Pressure control:** To implement PID control for precise pressure regulation. 
* The program assumes the existence of function blocks or functions for controlling the compressor, valve, and flow setpoint. 
* The cycle time of 100 ms should be adjusted based on the specific requirements of the system and the response time of the components. 
