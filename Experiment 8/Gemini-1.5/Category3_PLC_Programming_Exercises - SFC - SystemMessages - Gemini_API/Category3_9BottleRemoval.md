```
       ┌────┐      ┌────┐
       │    │      │    │
       │    │─────►│    │
       │    │      │    │
       │    │      │    │
       └────┘      └────┘
        INIT       EMPTY
                         │
                         │ No
                         ▼
                   ┌─────────────┐
                   │             │ Yes
                   │  DETECT    ◄─────┐
                   │             │     │
                   └─────────────┘     │
                         │              │ 
                         │ No           │ Bottle
                         ▼              ▼
                ┌─────────────┐  ┌─────────────┐
                │             │  │             │
                │  REJECT    │  │ PACKAGE   │
                │             │  │             │
                └─────────────┘  └─────────────┘
                         │              │
                         │              │
                         ▼              ▼
                   ┌─────────────┐  ┌────┐
                   │             │  │    │
                   │   WAIT     │  │    │
                   │             │  │    │
                   └─────────────┘  └────┘ 
```
**Description**

*   **INIT:** This is the initial step and is active when the program starts.
*   **EMPTY:**  This step checks if the bottle is empty using the proximity sensor for empty bottles. 
*   **DETECT:** This step checks if any bottle is detected by the proximity sensor. 
*   **REJECT:** If the bottle is empty, this step activates a cylinder to remove the bottle from the conveyor.
*   **PACKAGE:** If the bottle is not empty, this step initiates the packaging process.
*   **WAIT:**  This is the final step and the program waits here until a new bottle is detected. 

**Transitions**

*   The transition from INIT to EMPTY is always taken.
*   The transition from EMPTY to DETECT is taken if the bottle is not empty.
*   The transition from DETECT to REJECT is taken if the bottle is empty.
*   The transition from DETECT to PACKAGE is taken if the bottle is not empty. 
*   The transitions from REJECT and PACKAGE to WAIT are always taken.

**Note:** This SFC program is a basic example and may need to be modified or expanded depending on the specific requirements of the packaging system. For example, additional steps may be needed for different types of bottles or packaging materials. 
