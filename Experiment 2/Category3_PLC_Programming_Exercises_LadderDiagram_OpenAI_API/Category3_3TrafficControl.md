# Prompts

> Write a self-contained 61131-3 Ladder Diagram program, not a function block, to control a traffic light system. The system shall react to pedestrian push buttons and to the presence of emergency vehicles to give them priority.

# GPT4

To design a traffic light system that responds to pedestrian push buttons and gives priority to emergency vehicles in the framework of IEC 61131-3 using Ladder Diagram (LD) programming, I'll define the inputs and outputs, then proceed with the ASCII representation of the ladder logic according to these specifications.

### Inputs:
- `PB_Pedestrian`: Pedestrian Push Button (Bool)
- `Sens_Emergency`: Sensor for Emergency Vehicles (Bool)

### Outputs:
- `Light_Green`: Green Traffic Light (Bool)
- `Light_Yellow`: Yellow Traffic Light (Bool)
- `Light_Red`: Red Traffic Light (Bool)
- `Light_Pedestrian`: Pedestrian Crossing Light (Bool)

### Timers:
Given the environment of IEC 61131-3 does not directly depict timers in ASCII ladder logic, we will denote them as special function blocks for simplicity.
- `T_Green`: Timer for Green Light Duration
- `T_Yellow`: Timer for Yellow Light Duration
- `T_Red`: Timer for Red Light Duration
- `T_Emergency`: Timer for Emergency Vehicle Priority Duration (Short green time for emergency)

### Ladder Logic Representation:
Below is a simplified representation of the ladder logic in ASCII for the traffic light system. Note, in an actual automation project, the logic would include additional considerations for safety, sensor debouncing, and state transitions. Furthermore, actual ladder logic programming involves graphical elements that ASCII art cannot completely capture, so this serves as a conceptual illustration.

```plaintext
||(PB_Pedestrian)--[/]--(T_Green)--(Light_Yellow)--------------------------------||
||(Sens_Emergency)--[/]--(T_Emergency)-----(Light_Green)--------------------------||        
||                        --(Light_Yellow)--(T_Yellow)---------------------------||
||                                                     --(Light_Red)-------------||
||                             [T_Green]                                         ||
||                             --[T_Emergency]-----------------------------------||
||                                                     --[T_Yellow]              ||
||------------------------------------------------------------------------------(Light_Pedestrian)
||

Legend:
- || : Left Power Rail
- -- : Connection / Wire
- [/] : Normally Closed Contact (representing that the timer is not active)
- () : Coil
- [] : Timer has finished
```

### Discussion:
1. When the `PB_Pedestrian` is pressed and `T_Green` is not active, it will trigger the sequence transitioning from `Light_Green` to `Light_Yellow`, and then to `Light_Red`, allowing pedestrians to cross.
2. If `Sens_Emergency` is detected, `T_Emergency` triggers, providing a shortened cycle that prioritizes the emergency vehicle, briefly turning `Light_Green` on.
3. Timers are introduced to manage transitions between lights, ensuring there's no abrupt change that might confuse drivers and pedestrians.
4. This ASCII representation simplifies the logic to focus on key operations due to limitations in displaying complex ladder logic features in text format.
5. The pedestrians light (`Light_Pedestrian`) turns on when neither `Light_Green` nor `Light_Yellow` for vehicles is active, allowing safe crossing.

In a real-world application, this ASCII art would be translated into graphical ladder logic using a PLC programming tool, adhering to the IEC 61131-3 standard. This would include detailed configuration of timers, handling simultaneous inputs, and ensuring safe transitions between states.
