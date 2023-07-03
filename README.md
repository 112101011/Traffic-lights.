# Traffic-lights.

## Problem statement:
Implement a traffic light controller on Zybo. There is a highway and a crossroad, with a time counter, red and green traffic lights on each direction. When green light is on in one direction (say H: Highway), red is on in the other direction (say C: Crossroad), and the counter starts counting down from X to 0. Once the counter hits 0, the red traffic light should be on in H and green in C with the counter in C starting to count down from Y to 0. This should keep alternating. Come up with a nice state diagram, Verilog code at FSM abstraction and implement it on Zybo. <br/>
a) X and Y can be any number between 1 to 7. Use high value for highway counter and low value for crossroad counter to create more realistic scenario. <br/>
b) Take reset state to be highway green. <br/>
c) Use two 7-segment displays for displaying the counter values, red and green LEDs to display traffic lights. <br/>


## Description of approach:
X is taken as 7 and Y is taken as 5 here. There are two states as described in below picture <br/>
**State diagram:** <br/>
![image](https://github.com/112101011/Traffic-lights./assets/111628378/fbfdb097-058b-47f9-987c-66910eddf844)

First the reset pin will be clicked where highway green will be on, and both highway and crossroad count will be set to 7.and the next steps goes as follows: <br/>
Flow diagram: <br/>
![image](https://github.com/112101011/Traffic-lights./assets/111628378/31f25d6c-ae70-4e61-a9fa-d5741b1027d0)

Code, Port connections description:
1. In code module generate_1s is used to slow down the clock of zybo at L16 pin whose frequency is 125Mhz. That is done by counter. where the clk_1s is generated where for 62.5Mhz clk_1s is high and remaining 6.25MHz clk_1s is low.
2. The code is written such that whenever main road green is on cross road red will be on. And in both the signals the countdown goes from 7 to 0.
3. The code is written such that whenever cross road green is on main road red will be on. And in the both the signals the countdown goes from 5 to 0.
4. And this will repeat.

## Timing diagrams:

![image](https://github.com/112101011/Traffic-lights./assets/111628378/d610fb65-05c9-48c8-9abd-0decc4987457) <br/>


![image](https://github.com/112101011/Traffic-lights./assets/111628378/ca596077-78e7-4526-80fa-6643d0ca799b) <br/>

Observations:
From simulations we can infer that:
1) Whenever highway green is ON, highway red and crossroad green will be OFF, crossroad red will be ON. With countdown from 7
to 0 on both the signals.(that can be inferred from 7 segment display outputs displayH, displayM.
2) Whenever crossroad green is ON, highway green and crossroad red will be OFF, highway red will be ON. With countdown from 5
to 0. (that can be inferred from 7 segment display outputs displayH, displayM.

## Zybo implementation:
The first two LED’s green and red are for highway, next two LED’s are for cross road. Yellow LED is clk_1s. <br/>
Mainroad_state:(highway green)
![image](https://github.com/112101011/Traffic-lights./assets/111628378/200828b5-b47b-4518-ba47-7561953517ba)
Crossroad_state:(cross road green) <br/>
![image](https://github.com/112101011/Traffic-lights./assets/111628378/6c4b8c45-72c1-4ea2-b517-2cfedbb130c9)



Observations:
1) Whenever the system is in mainroad state, Green LED of highway is glowing and red LED of cross road is glowing, remaining bulbs will are in OFF. With countdowns from 7 to 0 on both seven segment displays.
2) Whenever the system is in crossroad state, Green LED of crossroad is glowing and red LED of highway is glowing, remaining bulbs will are in OFF. With countdowns from 5 to 0 on both seven segment displays.
