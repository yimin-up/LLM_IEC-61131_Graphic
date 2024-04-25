## Coffee Machine SFC Program (IEC 61131-3)

```
    +-----------------------+    +-----------------------+
    |                       |    |                       |
    | Initial Step (INIT)  |----| Coffee Only (COFFEE) |
    |                       |    |                       | 
    +--------+-------^------+    +--------+-------^------+
             |       |                    |       |
             |       |                    |       |
     +-------v-------+                    +-------v-------+
     |               |                    |               |
     |  Coffee &     |                    | Open Coffee   |
     |  Milk (CM)    |--------------------| Valve (OCV)   |
     |               |                    |               |
     +-------+-------+                    +-------+-------+
             |                                   |
             |                                   |
      +------v-------+                     +------v-------+
      |               |                     |               |
      | Open Milk     |---------------------| Wait 4 sec    |
      | Valve (OMV)   |                     | (TIMER)       |
      |               |                     |               |
      +-------+-------+                     +-------+-------+ 
             |                                   |
             |                                   |
      +------v-------+               +--------v--------+
      |               |               |                 |
      | Open Mixer    |---------------| Open Output     |
      | Valve (MXV)   |               | Valve (OPV)     |
      |               |               |                 |
      +-------+-------+               +--------+--------+
             |                                   |
             |                                   |
      +------v-------+               +--------v--------+
      |               |               |                 |
      | Start Mixer   |---------------| Close Output    |
      | Timer (MXT)  |               | Valve (CPV)     |
      |               |               |                 |
      +-------+-------+               +--------+--------+
             |                                   |
             |                                   | 
      +------v-------+               +--------v--------+
      |               |               |                 |
      | Check Mixer   |---------------| Close All      |
      | Level (CHKML) |               | Valves (CAV)   |
      |               |               |                 |
      +-------+-------+               +--------v--------+ 
             |                                   |
        +---v---+                               |
        |       |                               |
        | Mixer  |<------------------------------+
        | Full?  |
        |       |                                
        +-------+       

```

**Explanation:**

*   **Initial Step (INIT):** This is the starting point of the SFC. 
*   **Coffee & Milk (CM) / Coffee Only (COFFEE):** Based on the button pressed (Coffee & Milk or Coffee Only), the process branches to the respective path.
*   **Open Milk Valve (OMV):** If Coffee & Milk is selected, the milk valve opens. This step is skipped for Coffee Only.
*   **Open Coffee Valve (OCV):** The coffee valve opens in both cases.
*   **Open Mixer Valve (MXV):** The valve to the mixer opens, allowing the coffee and/or milk to flow.
*   **Start Mixer Timer (MXT):** A timer is started to control the mixing duration.
*   **Check Mixer Level (CHKML):**  This step checks if the mixer has reached its maximum level (130ml). 
*   **Mixer Full?:**  If the mixer is full, the process proceeds to close the coffee and milk valves and starts the 4-second mixing timer. Otherwise, it loops back to allow more liquid to enter the mixer.
*   **Wait 4 sec (TIMER):** The mixer operates for 4 seconds. 
*   **Open Output Valve (OPV):** The output valve opens to dispense the beverage.
*   **Close Output Valve (CPV):** After dispensing, the output valve closes.
*   **Close All Valves (CAV):** All valves (coffee, milk, mixer, and output) are closed, and the system returns to the initial step.

**Emergency Stop:**

The emergency stop button can be integrated into this SFC by adding a transition from each step to the INIT step, with the condition being the activation of the emergency stop button. This ensures that the process can be stopped immediately from any point in the operation. 

**Additional Considerations:**

*   **Sensors:** The SFC assumes the presence of sensors to detect the mixer level and the status of the valves. 
*   **Timers:** The specific implementation of timers may vary depending on the PLC platform.
*   **Error Handling:** Additional steps may be needed to handle errors, such as valve failures or tank overflow. 

**This SFC program provides a basic framework for the coffee machine operation. The specific implementation details may need to be adapted based on the chosen PLC platform and the desired level of complexity.** 
