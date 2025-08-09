# AWD Y Axis
Status: Complete - Documentation is in progress

## Proposal
The Y axis is underpowered. In comparison to the X axis, it is almost twice as slow in acceleration. This is due to having almost three times the load. Using multiple motors is not new and has been showcased successfully with other bed slingers, most notably the LH Stinger.

I propose to add an additional motor to the Y-axis by using Layer.shifted [Neptune 4/4pro Y-Axis Double Shear 9mm Belt Upgrade](https://www.printables.com/model/1208536-neptune-44pro-y-axis-double-shear-9mm-belt-upgrade) and mounting it in place of the Y-axis tensioner.

This modification also requires a new tensioner design and a way to automatically sync the two motors.

## Prerequists
The first order of business is to print, source, and build out The Y-Axis Double Shear. Once this is stable, then proceed to the next step. Remember to keep as much length of the belt as possible, you will need it when the additional motor is added.

### BOM
| QTY |  Item |
|-----|------------|
| 4 | M3 hex nuts (square should work too) |
| 4 | M3 x 40 hex sockethead cap screws |
| 1 | Mellow FLY adxl345 |
| 1 | USB cable (maybe 1 meter) |
| 2 | M3 x D5.0 x L4.0 heat inserts |
| 2 | M3 x 5 button or cap screws |
| 4 | M4 x 15 (I think) button head screws |

## Tensioner
Building the tensioner should be the second priority. My first iterations were printed from PETG, but after a few months, I found that it deformed badly under the pressure of the base plate mounting screws, and the belt retainers did. After redesigning the tensioner system to be more compact and include a spot for an adxl345, I printed this in ASA-CF. So far, it is holding just fine.

PETG Trials (pre adxl):
![image](https://github.com/user-attachments/assets/0d7da6f4-8fae-49e4-a98d-04bbaafb8e52)
![image](https://github.com/user-attachments/assets/c90b9249-b98b-47ea-a6e3-f3b157b50856)

ASA-CF (with Mellow Fly adxl345)
![image](https://github.com/user-attachments/assets/07147fa6-2a75-400a-81b3-49b518d19d3f)

ASA (with Mellow Fly adxl345) - Updated
![PXL_20250808_230447802](https://github.com/user-attachments/assets/19ac0813-5f43-4a9f-883a-129e881ef3a5)

## Second Motor
You need to add a MKS TMC2209 Stepper Motor Driver to the spare socket on your mainboard. Make sure to add the jumper to enable UART.
Adding the second motor is as simple as installing the first. 
- Bolt on the new Y tensioner to the bed
- Remove the stock Y tensioner, and mount the new motor using the same instructions.
- Find a suitable route for the motor wires and plug them into the driver pins.

## Adding Tension
There is a fore-and-aft tension system. 
- First, install the aft tensioner and install the screws so they grip onto the retaining nuts.
- Then install the front tensioner. Leave enough slack so you can start the screws into the retaining nuts.
- Slowly tighten the aft tensioner until there is 2mm of space. Then tighten the fore until you reach the desired frequency.

## Syncing the Motors
Syncing the motors is essential. If you do not the Input Shaping is unpredictable, and your steps will wear out faster as they play tug-of-war. You can either sync manually or automatically. Both ways work, however, the automatic way is slightly better.
- The manual approach is best described in the [LH Stinger documentation](https://github.com/lhndo/LH-Stinger/wiki/Tuning#awd-y-stepper-motor-sync).
- The automatic approach requires a dedicated adxl to be installed in the center of the base plate. I have used this [klipper plugin](https://github.com/MRX8024/motors-sync/tree/main) to accomplish the task of syncing. This guidance has been proven by the Voron core XY community.

## When to Sync the Motors
- You always need to sync the motors when you adjust the tension on the belt. Period. 
- With the automatic sync, you should also sync as part of your PRINT_START, because it's lazier to add it than to wonder if you should have added it.

## Tests
If I recall the dates correctly, I have the following

Single Y double shear
![image](https://github.com/user-attachments/assets/1b0bd6df-1da1-4ad1-b168-aa5ab56d5f23)

AWD manual sync
![image](https://github.com/user-attachments/assets/2bd41426-43d9-4049-b6bc-10cdda9f42f9)

AWD adxl sync + rigid spacers
![image](https://github.com/user-attachments/assets/2d773b66-4a9c-44ac-9af6-8e8d28dd4aef)

## Talk throughs
- [Part 1](https://www.youtube.com/shorts/GpRsdIZC7Hs)
- [Part 2](https://youtube.com/shorts/7Iwm1x9LCUw)
- [Part 3](https://youtube.com/shorts/XBzKG74UmCE)
- [Part 4](https://youtube.com/shorts/STW_UA8tv80)
- [Part 5](https://youtu.be/CL45KMCeoP4)
