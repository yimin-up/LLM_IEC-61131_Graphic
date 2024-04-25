## Underground Car Park Entry/Exit Control SFC Program

```
    +-------+    +-------+    +-------+    +-------+    +-------+
    | START |--->| S1    |--->| S2    |--->| S3    |--->| S4    |
    +-------+    +-------+    +-------+    +-------+    +-------+
                 |       ^    |       ^    |       ^    |       ^
                 |       |    |       |    |       |    |       |
                 |  M1   |    |  M3   |    |  M2   |    |  M4   |
                 V       |    V       |    V       |    V       |
    +-------+    +-------+    +-------+    +-------+    +-------+
    | S11   |--->| S21   |--->| S31   |--->| S41   |--->| S1    |
    +-------+    +-------+    +-------+    +-------+    +-------+
                 ^       |    ^       |    ^       |    ^       |
                 |       |    |       |    |       |    |       |
                 |  M20 -|----|  M30 -|----|  M20 -|----|  M30 -|
                 +-------+    +-------+    +-------+    +-------+ 
```

**Step and Action Descriptions:**

* **START:** Initial step, sets the green lights (Y2) ON and red lights (Y1) OFF.
* **S1:** Waiting for a car to enter from the ground floor (X1 is ON).
* **S11:** Car entering from ground floor.
    * Set M20 to ON (start of entry process).
    * Turn ON red lights (Y1) and turn OFF green lights (Y2).
* **S21:** Car passing through the passage from ground floor.
    * Wait for M20 to be OFF (car has completely passed).
* **S2:** Waiting for a car to enter from the basement (X2 is ON).
* **S31:** Car entering from basement.
    * Set M30 to ON (start of entry process).
    * Turn ON red lights (Y1) and turn OFF green lights (Y2).
* **S41:** Car passing through the passage from basement.
    * Wait for M30 to be OFF (car has completely passed).
* **S3:** Waiting for a car to exit to the ground floor (X2 is ON).
* **S4:** Waiting for a car to exit to the basement (X1 is ON).
* **Transitions:**
    * M1: Transition from S1 to S11 (car detected at ground floor entry).
    * M2: Transition from S3 to S11 (car detected exiting to ground floor). 
    * M3: Transition from S2 to S31 (car detected at basement entry).
    * M4: Transition from S4 to S31 (car detected exiting to basement).
    * M20 being OFF: Transition from S21 to S2 (car finished passing from ground floor).
    * M30 being OFF: Transition from S41 to S4 (car finished passing from basement).

**Additional Notes:**

* This program assumes the sensors (X1, X2) are only active for one scan cycle when a car passes. 
* The intermediate variables (M20, M30) ensure the red lights remain ON until the car completely passes through the passage.
* This is a basic example and can be further customized based on specific requirements such as timeouts, additional sensors, or different traffic light configurations.
* Ensure the PLC program is configured with appropriate timers and counters for the M and X variables according to the sensor and system specifications. 
