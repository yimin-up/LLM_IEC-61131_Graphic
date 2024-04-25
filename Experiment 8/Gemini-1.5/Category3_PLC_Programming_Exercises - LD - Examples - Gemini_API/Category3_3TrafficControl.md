## Traffic Light System in Ladder Diagram (LD)

Due to the complexity of a traffic light system with pedestrian and emergency vehicle interactions, it's best to break it down into smaller sections for clarity. Below is a possible implementation using LD:

**Global Variables:**

*   `PedestrianButton`: BOOL (Input) - Indicates pedestrian button press. 
*   `EmergencyVehicle`: BOOL (Input) - Indicates presence of emergency vehicle.
*   `TrafficLightState`: INT (Internal) - Stores the current state of the traffic light (e.g., 1 - Green Main Road, 2 - Yellow Main Road, 3 - Red Main Road & Green Pedestrian, etc.).
*   `Timer`: TON (Internal) - Timer for controlling light durations.

**Sections:**

1.  **Pedestrian Request:**

```
(Start of Ladder Diagram)
|                                                     |
|  PedestrianButton                              State  |
+-----| |---------------------------------------( )-----+
|                                                     |
|                    +-----------+                    |
|   State = 1        |    STL    |                    |
+-----| |---------|EN      ENO|---PedestrianRequest   |
|                    |           |                    |
|                    +-----------+                    |
|                                                     |
(End of Ladder Diagram)
```

This section sets a flag `PedestrianRequest` if the pedestrian button is pressed and the main road traffic light is green (State = 1). 

2.  **Emergency Vehicle Priority:**

```
(Start of Ladder Diagram)
|                                                        |
|  EmergencyVehicle                              State    |
+-----| |----------------------------------------( )-----+
|                                                        |
|                    +-----------+                      |
|   State <> 4       |    STL    |                      |
+-----| |---------|EN      ENO|---EmergencyVehicleRequest|
|                    |           |                      |
|                    +-----------+                      |
|                                                        |
(End of Ladder Diagram)
```

This section sets a flag `EmergencyVehicleRequest` if an emergency vehicle is present and the traffic light is not already in the emergency vehicle priority state (State <> 4).

3.  **State Machine:**

The state machine controls the traffic light sequence and reacts to the flags set in the previous sections. This section will be more complex and require several rungs to implement the logic for each state transition. 

**Example State Transition (Green Main Road to Yellow Main Road):**

```
(Start of Ladder Diagram)
|                                                                        |
|  State = 1     NOT PedestrianRequest  NOT EmergencyVehicleRequest   State   |
+-----| |---------+---------------------+-----------------------( )-----+
|                                                                        |
|                             +-----------+                              |
|                           |    TON    |                              |
+---------------------------|EN      ENO|---Timer                     |
|                             |           |                              |
|                        T#5S---|PT       ET|---                          |
|                             +-----------+                              |
|                                                                        |
|        Timer.Q                                                       2   | 
+----------------------------------------------------------------------( )-----+
|                                                                        |
(End of Ladder Diagram)
```

This example shows the transition from the Green Main Road state (State = 1) to the Yellow Main Road state (State = 2) after a 5-second timer (`T#5S`) expires, provided there are no pedestrian or emergency vehicle requests. Similar logic would be implemented for other state transitions.

4.  **Output Logic:**

This section uses the `TrafficLightState` variable to activate the corresponding outputs for each traffic light (e.g., green, yellow, and red lights for both main road and pedestrian crossing). 

**Important Considerations:**

*   **Safety**: This example provides a basic framework. A real-world implementation would require thorough safety analysis and additional logic to ensure safe operation and prevent hazardous situations.
*   **Timing**: The timer values and state durations should be adjusted based on specific traffic requirements and regulations. 
*   **Additional Features**: The system can be extended to include features like flashing yellow lights, turn signals, and different timings for peak and off-peak hours.

**Remember, this is a simplified example, and building a complete traffic light system requires careful consideration of safety, timing, and specific requirements.**
