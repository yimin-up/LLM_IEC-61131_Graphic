## Underground Car Park Entry/Exit Control SFC Program

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
        + M1                                            |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  EntryGround  |   |  S   |  M20       |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   |  Y1        |        |      |
|               |   |  R   |  Y2        |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + M3                                            |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
| EntryBasement |   |  S   |  M30       |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   |  Y1        |        |      |
|               |   |  R   |  Y2        |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + M4                                            |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|     Exit     |   |  R   |  M20       |        |      |
|               |---+------+------------+--------+      |
|               |   |  R   |  M30       |        |      |
|               |   |  N   |  Y1        |        |      |
|               |   |  S   |  Y2        |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + M2                                            |
        |                                               |
        |                                               |
        +----------------------->-----------------------+

(End of Sequential Function Chart)
```

**Explanation:**

* **Initial Step:** This step sets the initial state of the system with green lights (Y2) ON and red lights (Y1) OFF. 
* **EntryGround Step:** 
    * Triggered by M1 (car entering from ground floor).
    * Sets M20 to indicate ongoing ground floor entry process.
    * Turns ON red lights (Y1) and turns OFF green lights (Y2) to stop traffic in both directions.
* **EntryBasement Step:**
    * Triggered by M3 (car entering from basement).
    * Sets M30 to indicate ongoing basement entry process.
    * Turns ON red lights (Y1) and turns OFF green lights (Y2) to stop traffic in both directions.
* **Exit Step:** 
    * Triggered by either M4 (car exiting to ground floor) or M2 (car exiting to basement).
    * Resets M20 and M30 to indicate completion of entry process.
    * Turns ON green lights (Y2) and turns OFF red lights (Y1) to allow traffic flow.

**This SFC program controls the traffic lights based on car movement through the passage, ensuring safe and orderly entry/exit of vehicles.**
