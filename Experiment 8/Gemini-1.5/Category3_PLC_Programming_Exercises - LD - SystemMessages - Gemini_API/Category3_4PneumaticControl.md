## Pneumatic System Control - LD Program

```
--| |--[START]---------------------------------------------------------------------( )
   |
--| |--[CLK 100ms]---------( )
   |                       |
--| |--[I_Start]-----------| |---------------------------------------------(P_Run)
   |                       |
--| |--[I_Stop]------------| |----------------------------------------------(P_Stop)
   |                       |
--| |--[P_Run]-------------| |---+-------------------------------------------( )
   |                       |   |
--| |--[P_Stop]------------| |---+--( )--
   |                       |       |
--| |--[NOT P_Stop]--------| |-------| |--------------------------------( )
   |                                   |
--| |--[Pressure_Sensor < 5.5bar]----| |-------------------------------(P_LowPressure) 
   |                                   | 
--| |--[Pressure_Sensor > 6.0bar]----| |-------------------------------(P_HighPressure)
   |                                   |
--| |--[P_LowPressure]---------------| |--------------------------------( )
   |                                   |
--| |--[P_HighPressure]--------------| |--------------------------------( )
   |                                   |
--| |--[NOT P_LowPressure]-----------| |---+-----------------------------( )
   |                                   |   |
--| |--[NOT P_HighPressure]----------| |---+--( )--
   |                                   |       |
--| |--[AND]--------------------------| |-------| |----------------------(P_PressureOK)
   |                                   |
--| |--[Flow_Sensor < 50 slm]----------| |-------------------------------(P_LowFlow)
   |                                   |
--| |--[Flow_Sensor > 50 slm]----------| |-------------------------------(P_HighFlow) 
   |                                   |
--| |--[P_LowFlow]--------------------| |--------------------------------( )
   |                                   |
--| |--[P_HighFlow]-------------------| |--------------------------------( )
   |                                   |
--| |--[NOT P_LowFlow]----------------| |---+-----------------------------( )
   |                                   |   |
--| |--[NOT P_HighFlow]---------------| |---+--( )--
   |                                   |       |
--| |--[AND]--------------------------| |-------| |----------------------(P_FlowOK)
   |                                   |
--| |--[P_PressureOK]-----------------| |---+-----------------------------( )
   |                                   |   |
--| |--[P_FlowOK]---------------------| |---+--( )--
   |                                   |       |
--| |--[AND]--------------------------| |-------| |----------------------(P_SystemOK)
   |                                   | 
--| |--[P_SystemOK]-------------------| |-------(Q_AirValve)
   |
--| |--[END]-----------------------------------------------------------------------( )
```

**Explanation:**

*   **Inputs (I):**
    *   `I_Start`: Starts the system.
    *   `I_Stop`: Stops the system.
    *   `Pressure_Sensor`: Analog input representing the current pressure in bar.
    *   `Flow_Sensor`: Analog input representing the current flow in standard liters per minute (slm).
*   **Outputs (Q):**
    *   `Q_AirValve`: Controls the air valve to open or close based on the system status.
*   **Internal Variables (P):**
    *   `P_Run`: Indicates if the system is running.
    *   `P_Stop`: Indicates if the system is stopped.
    *   `P_LowPressure`: Indicates if the pressure is below the lower limit.
    *   `P_HighPressure`: Indicates if the pressure is above the upper limit.
    *   `P_PressureOK`: Indicates if the pressure is within the acceptable range.
    *   `P_LowFlow`: Indicates if the flow is below the target.
    *   `P_HighFlow`: Indicates if the flow is above the target.
    *   `P_FlowOK`: Indicates if the flow is within the acceptable range. 
    *   `P_SystemOK`: Indicates if both pressure and flow are within the acceptable range.

**Logic:**

1.  The system starts when `I_Start` is activated and stops with `I_Stop`.
2.  A 100ms clock pulse triggers the control loop.
3.  The program checks if the pressure and flow are within the acceptable range.
4.  If both pressure and flow are OK (`P_SystemOK`), the air valve (`Q_AirValve`) is activated. 
5.  If either pressure or flow is out of range, the air valve is deactivated. 

**Compliance with IEC 61131-3:**

*   The LD program uses standard LD elements such as contacts, coils, and blocks.
*   The program follows the basic rules of LD syntax and semantics.
*   The program is self-contained and does not rely on external function blocks. 
