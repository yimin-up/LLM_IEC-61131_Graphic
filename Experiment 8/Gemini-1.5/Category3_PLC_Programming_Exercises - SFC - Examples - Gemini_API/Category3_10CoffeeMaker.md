## Coffee Machine SFC

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
        + StartButton                                   |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|     Idle     |   |  N   |            |        |      | 
|               |---+------+------------+--------+      | 
|               |   |  N   | OpenValveCoffee |        |      | 
|               |   |  N   | OpenValveMilk   |        |      | 
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + CoffeeMilkButton                              | 
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  Coffee&Milk  |   |  N   |            |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | OpenValveMixer|        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + CoffeeButton                                  |
        |                                               |
        |                                               |
+---------------+                                       |
|    Coffee     |                                       |
|               |---+------+------------+--------+      |
|               |   |  N   | OpenValveMixer|        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + MixerFull                                     |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|   Mixing     |   |  N   | CloseValveCoffee |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | CloseValveMilk   |        |      |
|               |   |  N   | StartMixerTimer|        |      |
+---------------+   +------+------------+--------+      |
        |                                               |
        |                                               |
        + MixerTimerDone                                |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|  Dispensing   |   |  N   | OpenValveOutput|        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | StopMixer      |        |      |
+---------------+   +------+------------+--------+      | 
        |                                               |
        |                                               |
        + EmergencyStop                                 |
        |                                               |
        |                                               |
+---------------+   +------+------------+--------+      |
|   Emergency   |   |  N   | CloseAllValves |        |      |
|               |---+------+------------+--------+      |
|               |   |  N   | StopMixer      |        |      |
+---------------+   +------+------------+--------+      | 
        |                                               |
        |                                               |
        +----------------------->-----------------------+

(End of Sequential Function Chart) 
``` 
**Explanation:**

* **Initial Step:** The machine starts in the "Initial" step.
* **Idle Step:** Upon pressing the "StartButton," the machine transitions to the "Idle" step and opens both the coffee and milk valves. 
* **Coffee & Milk or Coffee Only Step:** Based on the button pressed ("CoffeeMilkButton" or "CoffeeButton"), the machine moves to the respective step and opens the mixer valve.
* **Mixing Step:** When the "MixerFull" sensor detects the mixer tank is full, the coffee and milk valves close, the mixer timer starts, and the machine enters the "Mixing" step.
* **Dispensing Step:** After the "MixerTimerDone" event, the output valve opens, the mixer stops, and the machine enters the "Dispensing" step.
* **Emergency Step:** If the "EmergencyStop" button is pressed at any point, the machine immediately transitions to the "Emergency" step, closing all valves and stopping the mixer. 

**Additional Notes:** 

* This SFC assumes the existence of functions like "OpenValveCoffee," "CloseAllValves," etc., which would control the respective actuators. 
* Error handling and additional functionalities like adjusting coffee/milk ratios or selecting different drink sizes can be further incorporated into the SFC. 
* The specific implementation of timers and sensors will depend on the chosen PLC platform. 
