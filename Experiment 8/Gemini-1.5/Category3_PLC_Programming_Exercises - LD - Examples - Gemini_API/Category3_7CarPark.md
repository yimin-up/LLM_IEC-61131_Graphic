## Underground Car Park Entry/Exit Control - Ladder Diagram

```
(Start of Ladder Diagram)
|                                                                                                                                   |
|  X1     M1                                                                                                                          |
+---| |---+-----------------------------------------------------------------------( )---M20-------------------------------------( )---+
|   |                                                                                                                                   |
|  X2     M3                                                                                                                          |
+---| |---+--------------------------------------( )---M30-------------------------------------------------------------( )---+
|   |                                                                                                                                   |
|  M20                                                                        M20                                                        |
+---|/|------------------------------------------(SET)---------------------------------------------------------(R)-------------------+
|   |                                                                                                                                   |
|  M30                                                                        M30                                                        |
+---|/|------------------------------------------(SET)---------------------------------------------------------(R)-------------------+
|   |                                                                                                                                   |
|  M1   M4                                                                                                                          |
+---| |---+---------------------------------------------------------------------------------------------------------(R)---M20--------+
|   |                                                                                                                                   |
|  M2   M3                                                                                                                          |
+---| |---+---------------------------------------------------------------------------------------------------------(R)---M30--------+
|   |                                                                                                                                   |
| M20  M30                                                               Y1                                                             | 
+---|/|---+---------------------------------------------------------------( )-----------------------------------------------( )---+
|   |                                                                                                                                   |
|NOT M20 NOT M30                                                        Y2                                                             |
+---|/|---+---------------------------------------------------------------( )-----------------------------------------------( )---+
|                                                                                                                                   |
(End of Ladder Diagram)
```

**Explanation:**

* **Sensor Inputs:** X1 and X2 trigger one-shot rising edge detection (M1, M2, M3, M4) to identify car entry from each direction. 
* **Entry Process Flags:** M20 and M30 are set when a car enters from the ground floor (X1 and not X2) or basement (X2 and not X1), respectively. They are reset when the car completely passes through (M4 for ground floor entry, M3 for basement entry).
* **Traffic Light Control:**
    * **Red Lights (Y1):** Activated when either M20 or M30 is ON, indicating a car is in the passage.
    * **Green Lights (Y2):** Activated when both M20 and M30 are OFF, indicating the passage is clear.

**This Ladder Diagram adheres to IEC 61131-3 standards and provides a safe and efficient control system for the underground car park entry/exit.** 
