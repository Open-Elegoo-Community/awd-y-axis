# AWD Y Axis
Status: Experimental - Documentation is in progress

## Proposal
The Y axis is underpowered. In comparison to the X axis, it is almost twice as slow in acceleration. This is due to having almost three times the load. The concept of using multiple motors is not new and has been showcased successfully with other bed slingers, most notably the LH Stinger.

I propose to add an additional motor to the Y axis by using Layer.shifted [Neptune 4/4pro Y-Axis Double Shear 9mm Belt Upgrade](https://www.printables.com/model/1208536-neptune-44pro-y-axis-double-shear-9mm-belt-upgrade) and mounted it in place of the Y axis tensioner.

This modification also requires a new tensioner design, and a way to automatically sync the two motors.

## Prerequists
The first order of business is to print, source, and build out The Y-Axis Double Shear. Once this is stable, the proceed to the next step. Remember to keep as much length of the belt as possible it will be needed when the additional motor is added.

## Tensioner
Building the tensioner should be the second priority. My first interations were printed from PETG, but after a few months I found that it deformed badly under the presure of the base plate mounting screws and the belt retainers did. After redesigning the tensioner system to be more compact and include a spot for an adxl345, I printed this in ASA-CF. So far, it is holding just fine.

PETG Trials (pre adxl):
![image](https://github.com/user-attachments/assets/0d7da6f4-8fae-49e4-a98d-04bbaafb8e52)
![image](https://github.com/user-attachments/assets/c90b9249-b98b-47ea-a6e3-f3b157b50856)

ASA-CF (with Mellow Fly adxl345)
![image](https://github.com/user-attachments/assets/07147fa6-2a75-400a-81b3-49b518d19d3f)

## Second Motor
You need to add a MKS TMC2209 Stepper Motor Driver to the spare socket on your mainboard. Make sure to add the jumper to enable UART.
Adding the second motor is as simple as installing the first. 
- Bolt on the new Y tensioner to the bed
- Remove the stock Y tensioner, and mount the new motor using the same instructions.
- Find a suitable route for the motor wires and plug it into the driver pins.

## Adding Tension
There is a fore-and-aft tension system. 
- First install the aft tensioner and install the screws so they grip on to the retaining nuts.
- Then install the front tensioner. Leave enough slack so you can start the screws into the retaining nuts.
- Slowly tighten the aft tensioner until there is 2mm of space. Then tighten the fore until you reach the desired frequency.

## Syncing the Motors
Syncing the motors is essential. If you do not the Input Shaping is unpredictable, and your steps will wear out faster as they play tug-of-war. You can either sync manually or automatically. Both ways work, however, the automatic way is slightly better.
- The manual approach is best described in the [LH Stinger documentation](https://github.com/lhndo/LH-Stinger/wiki/Tuning#awd-y-stepper-motor-sync).
- The automatic approach requires a dedicated adxl to be installed in the center of the base plate. I have used this [klipper plugin](https://github.com/MRX8024/motors-sync/tree/main) to accomplish the task of syncing. This guidance has been proven by the Voron core XY community.

## When to Sync the Motors
- You always need to sync the motors when you adjust the tension on the belt. Period. 
- With the automatic sync, you should also sync as part of your PRINT_START, because its lazier to add it than to wonder if you should have added it.

