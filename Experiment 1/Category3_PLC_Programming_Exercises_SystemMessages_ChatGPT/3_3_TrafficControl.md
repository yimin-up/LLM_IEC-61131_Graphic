# Prompts
> You are an AI expert in PLC (Programmable Logic Controller) programming. You are familiar with the international standard IEC 61131 for PLCs.
Your task is to write IEC 61131-3 Structured Text programs according to the requirements delimited by triple quotes.
'''
Write a self-contained 61131-3 structured text program, not a function block, to control a traffic light system. The system shall react to pedestrian push buttons and to the presence of emergency vehicles to give them priority.
'''
# ChatGPT
To create a Structured Text (ST) program for a traffic light system based on the IEC 61131-3 standard, we need to consider the various states of the traffic lights and the inputs from pedestrian push buttons and sensors for emergency vehicles. Here's an example of how such a program could be structured:

```pascal
PROGRAM TrafficLightControl
    VAR
        pedestrianButton : BOOL; // Input from pedestrian button
        emergencyVehicleSensor : BOOL; // Input from emergency vehicle sensor
        timer : TON; // Timer for light changes

        // Traffic light outputs (assume TRUE is light on)
        redLight : BOOL;
        yellowLight : BOOL;
        greenLight : BOOL;
    END_VAR

    // State enumeration for traffic light
    TYPE TrafficLightState : (
        RED, 
        GREEN, 
        YELLOW, 
        EMERGENCY
    );
    VAR
        currentState : TrafficLightState := TrafficLightState.RED;
    END_VAR

    // Constants for timing (in milliseconds)
    CONST
        greenTime : TIME := T#20s;
        yellowTime : TIME := T#5s;
        redTime : TIME := T#20s;
        emergencyTime : TIME := T#10s;
    END_CONST

    // Main program logic
    METHOD Main
        CASE currentState OF
            TrafficLightState.RED:
                // Red light on
                redLight := TRUE;
                yellowLight := FALSE;
                greenLight := FALSE;

                // Check for emergency vehicles
                IF emergencyVehicleSensor THEN
                    currentState := TrafficLightState.EMERGENCY;
                    timer(IN := TRUE, PT := emergencyTime);
                ELSIF timer.Q THEN
                    currentState := TrafficLightState.GREEN;
                    timer(IN := FALSE);
                END_IF;

            TrafficLightState.GREEN:
                // Green light on
                redLight := FALSE;
                yellowLight := FALSE;
                greenLight := TRUE;

                // Check for pedestrian button or timer
                IF pedestrianButton OR timer.Q THEN
                    currentState := TrafficLightState.YELLOW;
                    timer(IN := FALSE);
                END_IF;

            TrafficLightState.YELLOW:
                // Yellow light on
                redLight := FALSE;
                yellowLight := TRUE;
                greenLight := FALSE;

                // Change to red after yellow time
                IF timer.Q THEN
                    currentState := TrafficLightState.RED;
                    timer(IN := FALSE);
                END_IF;

            TrafficLightState.EMERGENCY:
                // Flashing red light for emergency
                redLight := NOT redLight; // Toggle red light
                yellowLight := FALSE;
                greenLight := FALSE;

                // Return to normal operation after emergency time
                IF timer.Q THEN
                    currentState := TrafficLightState.RED;
                    timer(IN := FALSE);
                END_IF;

        END_CASE;

        // Initialize timer for state changes
        IF currentState = TrafficLightState.RED AND NOT emergencyVehicleSensor THEN
            timer(IN := TRUE, PT := redTime);
        ELSIF currentState = TrafficLightState.GREEN THEN
            timer(IN := TRUE, PT := greenTime);
        ELSIF currentState = TrafficLightState.YELLOW THEN
            timer(IN := TRUE, PT := yellowTime);
        END_IF;
    END_METHOD
END_PROGRAM
```

This program sets up a simple state machine for the traffic light, handling four states: RED, GREEN, YELLOW, and EMERGENCY. The transitions between states are triggered by the timer, the pedestrian button, and the emergency vehicle sensor. Note that actual implementation might require additional safety considerations and integration with specific hardware.
