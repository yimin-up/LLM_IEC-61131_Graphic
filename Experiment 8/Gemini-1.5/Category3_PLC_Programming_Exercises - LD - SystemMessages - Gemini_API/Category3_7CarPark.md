## Ladder Diagram for Entry/Exit Control of Underground Car Park

```
--| |--[X1]----------( )---[M1]
--| |-----------------------|/|---+---[M20]
                                  |
--| |--[X2]----------( )---[M3]
--| |-----------------------|/|---+---[M30]

--| |--[M20]----------[Y1]
--| |--[M30]----------[Y1]

--| |--[M1]-----------(R)---|
--| |--[M4]-----------( )---|---[NOT Y1]
--| |-----------------------|/|---+---[Y2]
                                  |
--| |--[M2]-----------(R)---|
--| |--[M3]-----------( )---|---[NOT Y1]
--| |-----------------------|/|
```

**Explanation:**

* **Inputs:**
    * `X1` and `X2` are photoelectric sensors detecting car presence.
    * `M1`, `M2`, `M3`, and `M4` are one-shot rising edge detectors activated by the respective sensors. 
* **Intermediate Variables:**
    * `M20` is set when a car enters from the ground floor (`X1` is activated) and remains ON until the car exits.
    * `M30` is set when a car enters from the basement (`X2` is activated) and remains ON until the car exits.
* **Outputs:**
    * `Y1` controls the red lights. 
    * `Y2` controls the green lights.
* **Logic:**
    * When a car enters from the ground floor (`M1`), `M20` is set, turning ON the red lights (`Y1`).
    * Similarly, when a car enters from the basement (`M3`), `M30` is set, also turning ON the red lights (`Y1`).
    * Green lights (`Y2`) are turned ON only when neither `Y1` is ON, and either a car exits to the ground floor (`M4`) or to the basement (`M2`). This ensures only one direction of traffic is allowed at a time.
    * The `R` contact ensures `M20` and `M30` are reset when the car exits the passage, allowing the green lights to turn ON again when the passage is clear. 

**Compliance with IEC 61131-3:**

* The Ladder Diagram uses standard symbols for contacts, coils, and connections.
* The logic follows the allowed operations and connections within the LD standard. 
* The program adheres to the general rules of IEC 61131-3 for program structure and functionality. 
