## Temperature Control Ladder Diagram (LD)

```
--[ ]----------------------------------------------------( )----
   |                                                    |
--[ ]--[Sensor 1 > 22°C]--[Sensor 2 > 22°C]--[Sensor 3 > 22°C]--
   |                                                    |
--[ ]---------------------------------------( )----------+------
   |                                       |              |
--( )---------------------------------------+--------------+---
   |                                       |
--[ ]--[Sensor 1 < 20°C]--[Sensor 2 < 20°C]--[Sensor 3 < 20°C]--
   |                                       |
--[ ]---------------------------------------( )--------------
   |
--( )--[Heater ON]------------------------------------------
```

**Explanation:**

*   **Inputs:**
    *   Sensor 1, Sensor 2, Sensor 3: These represent the three temperature sensors providing input to the system. 
*   **Outputs:**
    *   Heater ON: This output controls the power to the heating system.
*   **Logic:**
    *   The upper rung checks if any of the sensors detect a temperature above 22°C. If any sensor reads above the threshold, the rung is true, and the output remains off.
    *   The lower rung checks if all sensors detect a temperature below 20°C. If all sensors read below the threshold, the rung is true, and the output turns the heater on. 
    *   This logic ensures the heater only activates when all sensors agree the temperature is below the desired range and deactivates when any sensor detects a temperature above the desired range.

**Compliance with IEC 61131-3:**

*   The LD uses standard symbols for contacts and coils as defined in the standard.
*   The logic follows the allowed connections and branching rules.
*   The program is self-contained and does not require any additional function blocks.

**Additional Considerations:**

*   This is a basic example and may require modifications depending on the specific heating system and sensor types.
*   Additional logic could be added for safety features, alarms, or more complex control strategies.
*   Timers or counters could be incorporated to introduce delays or hysteresis to the system. 
