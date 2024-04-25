```
--| |-------------------| |--
  |                        |
  |                        PB1: Proximity sensor detects any bottle 
  |                        
--| |-------------------| |--
  |                        |
  |--| |-----------------( )--
     |                   PB2: Proximity sensor detects only empty bottles
  |--| |-----------------( )-- 
  |                        |
  |                        | 
--| |-------------------| |--
  |                        |
  |                        |
  |--( )-----------------( )--
     CYLINDER: Removes empty bottles
  |--( )-----------------( )-- 
  |                        |
--| |-------------------| |--     
```
**Explanation:**

*   The left and right power rails are represented by `--| |--`.
*   `PB1` and `PB2` are input variables representing the proximity sensors. 
*   `CYLINDER` is an output variable representing the cylinder that removes empty bottles.
*   The normally open contact `--| |--` is used for the normally open proximity sensors.
*   The coil `--( )--` is used to activate the cylinder.
*   The empty bottle removal system is activated only when both conditions are met: 
    *   A bottle is detected (PB1 is ON).
    *   The bottle is empty (PB2 is ON). 
    
**Additional Considerations:**

*   You may need to add additional logic to handle cases such as:
    *   What happens when a bottle gets stuck?
    *   How to handle different bottle sizes?
    *   How to integrate with other parts of the packaging line?
*   This is a basic example, and the actual implementation may vary depending on the specific requirements of your application. 

