## Elevator Control with Ladder Diagram

Due to the complexity of a 5-floor elevator system, the complete Ladder Diagram would be extensive and involve numerous rungs and variables. However, I can provide you with a structural outline and key components to guide you in building the program:

**Global Variables:**

*   **CurrentFloor:** INT (0-4 representing floors)
*   **TargetFloor:** INT (0-4)
*   **Direction:** BOOL (0 - Down, 1 - Up)
*   **DoorTimer:** TON (Preset 7s)
*   **IdleTimer:** TON (Preset 10s)
*   **FloorButtonsUp:** ARRAY[0..4] OF BOOL 
*   **FloorButtonsDown:** ARRAY[0..4] OF BOOL
*   **CabinButtons:** ARRAY[0..4] OF BOOL

**Main Program Structure:**

1.  **Floor Detection:**
    *   Use limit switches for each floor (top and bottom) to update the `CurrentFloor` variable. 

2.  **Target Floor Determination:**
    *   Evaluate `FloorButtonsUp`, `FloorButtonsDown`, and `CabinButtons` to determine the next target floor (`TargetFloor`) based on current direction and button presses.
    *   Implement logic to prioritize cabin buttons over floor buttons.
    *   Adjust `Direction` based on `CurrentFloor` and `TargetFloor`.

3.  **Movement Control:**
    *   Based on `Direction`, activate the appropriate motor control relays (Up or Down). 
    *   Stop the motor when `CurrentFloor` equals `TargetFloor`.

4.  **Door Control:**
    *   When arriving at `TargetFloor`:
        *   Start `DoorTimer`.
        *   Open doors while `DoorTimer.Q` is active.
        *   If any `CabinButtons` are pressed during this time, reset `DoorTimer` and `IdleTimer`.
        *   If no buttons are pressed and `DoorTimer` finishes, start `IdleTimer`.
        *   If `IdleTimer` finishes, close the doors.

5.  **Safety Interlocks:** 
    *   Implement safety checks to prevent door operation while the elevator is moving.
    *   Ensure proper stopping at the top and bottom floors.

**Ladder Diagram Snippets (Examples):**

**Floor Detection:**

```
(Start of Ladder Diagram)
|                                         |
|   TopLimitSwitch[2]   CurrentFloor      |
+-------| |--------------( )---2----------+
|                                         |
|   BottomLimitSwitch[2] CurrentFloor     |
+-------| |--------------( )---2----------+
|                                         |
(End of Ladder Diagram)
```

**Door Timer:**

```
(Start of Ladder Diagram)
|                                             |
|    TargetFloorReached  DoorTimer.IN        |
+--------| |-----------------| |-------------+
|                                             |
|    CabinButtonPressed  DoorTimer.RESET      |
+--------| |-----------------| |-------------+
|                                             |
|   DoorTimer.Q          OpenDoorRelay       | 
+--------| |-----------------| |-------------+
|                                             |
(End of Ladder Diagram)
```

**Remember:** This is a simplified overview. The actual implementation will require detailed logic for each function and handling various edge cases. 

**Additional Considerations:**

*   **Visualization:** Consider using HMI (Human Machine Interface) software to visualize elevator status, floor buttons, and other relevant information.
*   **Advanced Features:** You can incorporate features like emergency stop, overload detection, and different operating modes (e.g., fireman mode).

**By combining these components and expanding on the logic, you can develop a comprehensive Ladder Diagram program for your 5-floor elevator system.**
