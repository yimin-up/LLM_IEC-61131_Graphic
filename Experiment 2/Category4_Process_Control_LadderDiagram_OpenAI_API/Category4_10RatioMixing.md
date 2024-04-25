# Prompts

> Write a self-contained 61131-3 Ladder Diagram program, not a function block, to implement ratio control for mixing two reactants in a 2 to 1 ratio.

# GPT4

Creating a Ladder Diagram in ASCII for ratio control to mix two reactants in a 2 to 1 ratio involves several steps, including setting up control for two pumps or valves that regulate the flow of the reactants. For simplicity, let's assume each reactant flow is controlled by a digital output (valve or pump) from the PLC: Reactant A (PumpA) and Reactant B (PumpB). The goal is to ensure that for every unit of Reactant B, two units of Reactant A are added. 

Note: In a real-world application, flow meters would provide feedback to the PLC to accurately control the ratio, and PID controllers might be used to fine-tune the flow rates. However, without the ability to create function blocks or simulate real-time feedback in simple ASCII art Ladder Diagram, the design will be conceptual and assumes the pumps/valves have linear flow characteristics and can be controlled just by turning them on/off in sequence.

This ASCII art Ladder Diagram represents a simplified version of the control logic needed:

```
  Start/Stop       ReactantB_Control    ReactantA_Control   Timer   ReactantA_DoubleControl
     |                     |                  |              |               |
    [ ]-------+-----------[ ]---------------[ ]-------------[ ]-------------[ ]-------
     Start    |   Stop     |      Cont_B     |     Cont_A    |    Timer    ReactA_x2
              |            |                 |               |
              +-[ ]--------+                 +------------[ ]--------------+
                 Stop                                         Timer_Done
```

Explanation of symbols and their ASCII representations:
- `[ ]` is a normally open (NO) contact
- `+` and `|` are used to represent wires or electrical connections

In this diagram:
- The first line represents the start-stop logic. The system starts when the Start button is pressed and stops when the Stop button is pressed.
- The second [ ] (NO contact) named `ReactantB_Control` (Cont_B) represents the control for Reactant B's pump/valve. When activated, it will allow Reactant B to flow.
- The third [ ] (NO contact) named `ReactantA_Control` (Cont_A) represents the control for Reactant A's pump/valve. It ensures Reactant A flows concurrently with Reactant B.
- The fourth [ ] (NO contact) represents a timer used to control the duration of Reactant A's flow to achieve the 2:1 ratio. When the timer completes, it triggers the `ReactantA_DoubleControl` (ReactA_x2) to stop Reactant A's flow.
- The last condition highlights a sequence where Reactant A needs to be doubled in comparison to Reactant B, managed by `ReactA_x2`. Once the Timer indicating a complete cycle for Reactant A to ensure the 2:1 ratio is achieved, the system cycles back, potentially for another batch, based on the start/stop conditions and the duration set by the Timer.

In reality, integration with analog inputs from flow meters and possibly PID loop control for the pumps would be required for precise control of the reactant flow rates. This ASCII diagram simplifies these components to illustrate basic logic.
