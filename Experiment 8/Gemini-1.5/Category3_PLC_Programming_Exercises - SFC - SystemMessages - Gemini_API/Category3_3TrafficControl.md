## Traffic Light Control - SFC Program

```
   ┌─────┐    ┌─────┐    ┌─────┐    ┌─────┐
   │ INIT│────>│ S1  │────>│ S2  │────>│ S3  │
   └─────┘    └─────┘    └─────┘    └─────┘ 
       │         │         │         │
       │         │         │         │
       │    +─────┘         │         │
       │    │              │         │
       │    │   ┌─────┐    │         │
       │    │   │ S4  │    │         │
       │    └────>│     │<───┘         │
       │         └─────┘              │ 
       │                             │  
       │   ┌────────────────────┐    │  
       │   │                    │    │ 
       │   ▼                    │    │
       │┌─────┐    ┌─────┐    ┌─────┐ 
       ││ S5  │────>│ S6  │────>│ S7  │ 
       │└─────┘    └─────┘    └─────┘ 
       │         │         │         │
       │         │         │         │
       │    +─────┘         │         │
       │    │              │         │
       │    │   ┌─────┐    │         │
       │    │   │ S8  │    │         │
       │    └────>│     │<───┘         │
       │         └─────┘              │
       │                             │
       └────────────────────────────┘
```

**Step Descriptions:**

* **INIT:** Initial step. Sets initial states of the traffic lights and variables. 
* **S1:** Green light for vehicles on the main road.
* **S2:** Yellow light for vehicles on the main road.
* **S3:** Red light for vehicles on the main road, green light for pedestrians.
* **S4:** Red light for vehicles on the main road, flashing green light for pedestrians (indicates the walk signal will soon change). 
* **S5:** Red light for vehicles and pedestrians on the main road, green light for vehicles on the side road.
* **S6:** Yellow light for vehicles on the side road.
* **S7:** Red light for vehicles on the side road. 
* **S8:** Red light for vehicles on the side road, flashing green light for vehicles on the main road (indicates the traffic signal will soon change).

**Transitions:**

* **INIT to S1:** Always transition after initialization.
* **S1 to S2:** Transition after a set time or if an emergency vehicle is detected.
* **S2 to S3:** Transition after a set time.
* **S3 to S4:** Transition after a set time or if the pedestrian button is pressed.
* **S4 to S5:** Transition after a set time.
* **S5 to S6:** Transition after a set time or if an emergency vehicle is detected on the side road.
* **S6 to S7:** Transition after a set time.
* **S7 to S8:** Transition after a set time or if the pedestrian button is pressed again.
* **S8 to S1:** Transition after a set time.
* **Any state to S5:** Transition immediately if an emergency vehicle is detected on the main road.

**Actions:**

* Each step activates the corresponding traffic lights and pedestrian signals.
* Timers are started and stopped as needed for each step.
* Emergency vehicle detection is continuously monitored.
* Pedestrian button presses are monitored.

**Additional Notes:**

* This is a basic example and can be extended to include additional features such as multiple lanes, turn signals, and adaptive timing based on traffic flow.
* The specific timing values and logic for emergency vehicle detection will need to be adapted to the specific application.
* This example utilizes the SFC language. The actual implementation may require additional function blocks for timers, input/output handling, and other functionalities. 

**Please note that this is a textual representation using ASCII art. The actual implementation would require a proper IEC 61131-3 compliant programming environment.** 
