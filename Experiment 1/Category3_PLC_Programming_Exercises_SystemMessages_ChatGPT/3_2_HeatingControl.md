# Prompts
> You are an AI expert in PLC (Programmable Logic Controller) programming. You are familiar with the international standard IEC 61131 for PLCs.
Your task is to write IEC 61131-3 Structured Text programs according to the requirements delimited by triple quotes.
'''
Write a self-contained 61131-3 structured text program, not a function block, to control the temperature of a heating system. The system should automatically turn on and off based on three temperature sensors and maintain a constant temperature range between 20 and 22 degree celsius.
'''
# ChatGPT
To create a Structured Text (ST) program according to the IEC 61131-3 standard for controlling a heating system, we need to consider the following requirements:

The system should read from three temperature sensors.
It should maintain the temperature within a range of 20 to 22 degrees Celsius.
The heating system should automatically turn on and off to maintain this temperature range.
Here is a basic example of how such a program might look:

```iec
PROGRAM HeatingControl
    VAR
        Sensor1, Sensor2, Sensor3: REAL;  // Temperature readings from the sensors
        AverageTemp: REAL;               // Average temperature from the sensors
        HeaterOn: BOOL;                  // Heater status
    END_VAR

    // Main control logic
    AverageTemp := (Sensor1 + Sensor2 + Sensor3) / 3.0;

    IF AverageTemp < 20.0 THEN
        HeaterOn := TRUE;   // Turn on the heater if the average temperature is below 20 degrees
    ELSIF AverageTemp > 22.0 THEN
        HeaterOn := FALSE;  // Turn off the heater if the average temperature is above 22 degrees
    END_IF;
END_PROGRAM
```

This program performs the following actions:

Data Acquisition: It reads the temperature values from three sensors (Sensor1, Sensor2, Sensor3).
Processing: It calculates the average temperature from these three sensors.
Control Logic:
If the average temperature is below 20 degrees Celsius, the heater is turned on (HeaterOn := TRUE).
If the average temperature exceeds 22 degrees Celsius, the heater is turned off (HeaterOn := FALSE).
This example assumes that the temperature sensors are properly connected and their readings are available to the PLC. Also, the variable HeaterOn would typically be connected to a physical output controlling the heating system. The actual implementation might require more details based on the specific hardware and system configuration.
