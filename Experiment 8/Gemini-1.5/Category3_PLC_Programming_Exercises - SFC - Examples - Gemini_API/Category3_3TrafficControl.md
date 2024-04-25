```
(* Start of Sequential Function Chart *)

        +----------------------<------------------------+
        |                                               |
        |                                               |
+============+                                          |
||          ||                                          |
||  Init   ||                                          |
||          ||                                          |
+============+                                          |
        |                                               |
        |                                               |
        + Emergency or Pedestrian                      |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  Prep_Stop   |   |  N   | Tmr_Stop (=5) |        |      | 
|               |---|      |            |        |      |
|               |   |      |            |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + Tmr_Stop.Q                                    |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|    Stop      |   |  N   | Red        |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | Yellow     |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | Tmr_Clear (=3) |        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + Tmr_Clear.Q                                   |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  Prep_Go    |   |  N   |  Tmr_Go (=10) |        |      |
|               |---|      |            |        |      |
|               |   |      |            |        |      | 
+---------------+   +------+------------+--------+      | 
        |                                               |
        |                                               |
        + Tmr_Go.Q                                     |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|      Go     |   |  N   |  Green      |        |      |
|               |---+------+------------+--------+      | 
|               |   |  N   |  Yellow     |        |      | 
|               |---+------+------------+--------+      | 
|               |   |  N   |  Tmr_Go (=10) |        |      | 
+---------------+   +------+------------+--------+      | 
        |                                               |
        |                                               | 
        + NOT Emergency and NOT Pedestrian            |
        |                                               |
        |                                               |
        +----------------------->-----------------------+

(* End of Sequential Function Chart *) 
``` 
**Explanation:**

*   **Init:** This is the initial step where the system is initialized.
*   **Emergency or Pedestrian:** This transition checks if there is an emergency vehicle approaching or if a pedestrian has pressed the button.
*   **Prep\_Stop:** This step prepares the traffic light to stop by activating a timer (Tmr\_Stop) for 5 seconds. 
*   **Stop:** This step activates the red light and then the yellow light for 3 seconds (Tmr\_Clear), preparing for the green light.
*   **Prep\_Go:**  This step prepares the traffic light to go by activating a timer (Tmr\_Go) for 10 seconds.
*   **Go:** This step activates the green light, then the yellow light, and sets the timer for the green light again. 
*   **NOT Emergency and NOT Pedestrian:** This transition checks if there's no emergency and no pedestrian requesting to cross, in which case the system continues the normal green-yellow-red cycle. 

**Additional Considerations:**

*   The timers' durations (Tmr\_Stop, Tmr\_Clear, Tmr\_Go) can be adjusted as needed. 
*   This SFC program can be expanded to include additional states and transitions to handle more complex traffic light scenarios. 
*   Input variables: Emergency (Boolean), Pedestrian (Boolean)
*   Output variables: Red (Boolean), Yellow (Boolean), Green (Boolean) 
