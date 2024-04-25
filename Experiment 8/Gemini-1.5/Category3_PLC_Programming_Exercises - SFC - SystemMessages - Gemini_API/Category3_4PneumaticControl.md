## Pneumatic System Control SFC Program

```
   +-------+    +---+    +------+    +---+    +-------+
 --| INIT |--->| S1 |--->| FILL |--->| S2 |--->| IDLE |---
   +-------+    +---+    +------+    +---+    +-------+
        ^          |           |           |          |
        |          +-----------+-----------+          |
        +---------------------------------------------+

**INIT Step:**
*   Set initial values for variables:
    *   `flow_rate` = 0
    *   `pressure` = 0

**S1 Step:**
*   Check input signal for air flow request:
    *   If TRUE: transition to FILL step
    *   If FALSE: remain in S1

**FILL Step:**
*   Start air flow to actuators.
*   Control flow rate to reach 50 standard liters per minute.
*   Monitor pressure:
    *   If pressure reaches 6 bar: transition to S2
    *   If pressure remains below 5.5 bar after a timeout period (e.g., 5 seconds): trigger alarm and transition to IDLE.

**S2 Step:**
*   Maintain pressure between 5.5 and 6 bar by adjusting the air flow rate. 
*   Check input signal for air flow request:
    *   If FALSE: transition to IDLE step
    *   If TRUE: remain in S2

**IDLE Step:**
*   Stop air flow to actuators.
*   Wait for input signal requesting air flow.
    *   If TRUE: transition to FILL step
    *   If FALSE: remain in IDLE

**Additional Notes:**
*   This SFC program uses a control loop frequency of 100ms. 
*   The timeout period in the FILL step can be adjusted based on system requirements.
*   Alarm handling and specific control mechanisms for flow and pressure regulation are not explicitly detailed in this SFC but should be implemented using appropriate function blocks or additional steps as needed.
*   This program assumes the presence of sensors for pressure and flow rate, and actuators for controlling the air flow.
``` 
