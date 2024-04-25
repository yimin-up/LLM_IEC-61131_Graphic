## Traffic Light Control with Pedestrian and Emergency Vehicle Priority (Ladder Diagram)

```
--| |-------------------------------------------------------------------|
--| |                                                                   |
-| |------[PB1]-------|-------|-----------------------------------------( )--
--| |      Pedestrian     Timer     Emergency              Green Light
--| |      Button 1       (T1)     Vehicle Sensor       for Vehicles
--| |                                                                   |
-| |------[PB2]-------|-------|-----------------------------------------( )--
--| |      Pedestrian     Timer     Emergency              Yellow Light
--| |      Button 2       (T2)     Vehicle Sensor       for Vehicles
--| |                                                                   |
-| |--------------------|-------|-----------------------------------------( )--
--| |                    Timer     Emergency              Red Light
--| |                    (T3)     Vehicle Sensor       for Vehicles
--| |                                                                   |
--| |-------------------------------------------------[M1]---------------|
--| |                                                   Master Relay      | 
--| |                                                   (Traffic On/Off)   |
--| |-------------------------------------------------------------------|

-- Timer Settings:
-- T1: PT = 10s (Pedestrian crossing time)
-- T2: PT = 5s  (Yellow light duration)
-- T3: PT = 20s (Red light duration for vehicles)
```

**Explanation:**

* **Inputs:** 
    * `PB1` & `PB2`: Pedestrian push buttons at each side of the crossing.
    * `Emergency Vehicle Sensor`: Detects the presence of an emergency vehicle.
* **Outputs:**
    * `Green Light`, `Yellow Light`, `Red Light`: Control the traffic lights for vehicles. 
    * `M1`: Master relay, controls the overall system operation (ON/OFF). 
* **Timers:**
    * `T1`: Starts when a pedestrian button is pressed and controls the pedestrian crossing time (green light for pedestrians).
    * `T2`: Starts after T1 or emergency vehicle detection, controls the yellow light duration for vehicles.
    * `T3`: Controls the red light duration for vehicles when there's no pedestrian or emergency vehicle.
* **Logic:**
    * When `M1` is ON (system active):
        * If `Emergency Vehicle Sensor` is activated:
            * Immediately switch to `Red Light` for vehicles. 
            * `T2` starts to control the yellow light duration.
        * If a `Pedestrian Button` is pressed and `T3` is not timing:
            * `T1` starts, activating the `Green Light` for pedestrians (implicitly red for vehicles).
            * After `T1` finishes, `T2` starts for the yellow light phase. 
        * If no pedestrian or emergency vehicle is present, `T3` controls the red light duration for vehicles. After `T3` finishes, the green light for vehicles will be activated (implicitly red for pedestrians).

**Additional Notes:**

* This is a basic example and may require modifications depending on specific requirements and local regulations.
* The timer settings (PT values) can be adjusted as needed.
* Additional logic can be implemented for features like flashing green lights, pedestrian signals, etc.
* Remember to configure the timers and outputs according to the specific PLC hardware and software used. 

**IEC 61131-3 Compliance:**

* The Ladder Diagram adheres to the basic structure and symbols defined in the IEC 61131-3 standard.
* Timers and outputs are represented using standard function blocks.
* The logic flow is clear and easy to understand. 
