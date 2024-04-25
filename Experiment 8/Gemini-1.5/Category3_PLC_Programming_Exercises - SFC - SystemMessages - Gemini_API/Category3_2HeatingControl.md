## Heating System Temperature Control - SFC Program

```
    +-------------------+    +------------+    +------------+    +-------------+
    |       INIT       |    |  CheckTemp  |    |   HeatOn   |    |  HeatOff   | 
    +--------+--------+    +-----+------+    +-----+------+    +-----+------+
             |                     |                   |                   |
             | T1 > 22 or T2 > 22 or| T1 < 20 and T2 < 20| Temp >= 22      | Temp <= 20 
             | T3 > 22              | and T3 < 20       |                  |
             +--------------------->+                   +---------------->+
             |                     |                   |                   |
             |     T1 <= 22 and    |                   |                   |
             |     T2 <= 22 and    |                   |                   |
             |     T3 <= 22        |                   |                   |
             +--------------------->+                   +---------------->+ 
                                    |                                   |
                                    +-----------------------------------+

```
**Explanation:**

*   **INIT:** This is the initial step that starts the program. 
*   **CheckTemp:** This step checks the temperature readings from three sensors (T1, T2, T3).
    *   If any sensor reads a temperature above 22°C, the program transitions to the "HeatOff" step.
    *   If all sensors read temperatures below 20°C, the program transitions to the "HeatOn" step.
    *   If the temperatures are within the desired range (20-22°C), the program remains in the "CheckTemp" step.
*   **HeatOn:** This step turns on the heating system and remains active as long as the temperature is below 20°C.
*   **HeatOff:** This step turns off the heating system and remains active as long as the temperature is above 22°C. 

**Compliance with IEC 61131-3:**

*   The SFC program uses standard symbols for steps, transitions, and actions.
*   The transitions are defined with logical conditions based on temperature readings.
*   The actions in "HeatOn" and "HeatOff" steps directly control the heating system. 

**Additional Considerations:**

*   This is a basic example and can be extended to include more complex logic, such as hysteresis control or different temperature setpoints for different zones.
*   Error handling and safety measures should be implemented in a real-world application. 
*   The specific implementation of actions (e.g., turning on/off the heating system) will depend on the PLC hardware and connected devices. 
