# Description
Because original external feeder for Sovol SV08 MAX is (being direct) horrible I created this project to adress some issues. I treat this as self-development project so I not guaranteeing that it would work on your setup, but despite this I'm open to sugestions. For now everything is tested only on PLA setup.

# Quick look on setup
## IRL photos
![559814326_4341665236066659_7573989402878520107_n](https://github.com/user-attachments/assets/13d1012b-2f81-4489-8f28-96c8f767a857)![559183310_4341665459399970_7819196083902323529_n](https://github.com/user-attachments/assets/96154bac-ef33-40ed-82b7-8d8d39306e26)

## Models

<img width="1078" height="815" alt="image" src="https://github.com/user-attachments/assets/94a5c181-8fe6-4dc3-9996-11a2b86c1c14" />
<img width="620" height="539" alt="image" src="https://github.com/user-attachments/assets/46c2c6be-7fda-4736-896b-82629bf09ebe" />
<img width="579" height="502" alt="image" src="https://github.com/user-attachments/assets/aa882729-d9f8-4234-8a25-86bd82573f90" />

## Tutorial
If you want just bare minimum you have to print custom enclosure for external feeder (in **ABS!!!**). (other matierals would melt). Internal stepper motor gets realy hot and can overheat MCU.
### Hardware needed
* 8x M5 nuts and bolts(40mm)
* 4x threaded insert M3 5mm or 3mm
* 2x M3 bolt 12mm(or longer)
* 4x bearing 608 ZZ 8x22x7mm
* wooden countertop 800mmx400mmx18mm
* 1.5m of any cable capable of transfer power and signal to external feeder

### Step by step
#### Hardware
1) Before printing enclosure for external feeder use "BearingCheck.step" to test if model printed from your printer is a perfect fit, bearing must fit perfectly to ensure smooth filament passage. If not try to adjust offsets until bearings fit and apply them to the CustomFeederCase.step.

2) Print external feeder enclosure in **ABS!!!**. Other materials would soften or worse even melt. Use supports for latches and overhangs.

3) Print every other part in PLA.

4) Those 2 elements might be lose, if so, apply some glue in socket <img width="709" height="461" alt="image" src="https://github.com/user-attachments/assets/942b7660-bf55-49f1-864d-5afe315b58b7" />

5) Put 4 inserts according to image <img width="1101" height="491" alt="image" src="https://github.com/user-attachments/assets/09866b18-5ee6-4361-a7ef-26ac0b24adc3" />

6) Drill contertop to allow mount of FeederMount.step, TopSpoolMount.step and TopDeckGlassMount.step, the suggested arangment is on photo below, mouting spool on the right shorten the length of PTFE tube. Assembly and mount parts.<img width="4080" height="1884" alt="image" src="https://github.com/user-attachments/assets/c680c8ee-d974-43c3-b17c-4f200b404bdb" /><img width="1194" height="895" alt="image" src="https://github.com/user-attachments/assets/128d7f71-f5b2-46d5-9856-e67ee444517b" />

7) To hold spool on rollers you can use anything cylindrical strong enough (I used curtain rod xD), but be aware that shaft shift so aditional stoppers may be needed.

#### Software

1) Replace buffer_stepper.cfg
2) Remove references to old buffer macros from Macro.cfg, example how to do it is inside example_Macro.cfg
3) There are 2 things inside buffer_stepper.cfg that may need adjustment:
   * variable_default_rotation_distance: 9.75 (this is rotation_distance in mm for buffer stepper recalculations)
   * variable_filament_length_ptfe: 1300.0 (this is length in mm between toolehad extruder and buffer)
4) Add INIT_CYCLIC_MACROS after CLEAR_PAUSE inside START_PRINT macro
5) Add CENTER_EXTERNAL_FEEDER after INIT_CYCLIC_MACROS
6) Add RESET_VARIABLES_BUFFER_STEPPER at the end of END_PRINT and CANCEL_PRINT macros


# Versions
## List
* V0.1
    * Initial macro for resynchronization
    * Initial macro for filament runout detectiom
    * Initial versions of step filest for mod
### Known issues for V0.1
* V0.1
  * If for some reason filament inside buffer slips right after buffer recalculation, it will lead to big change in rotation and possibly constant recalculation those will block printing progress until method SET_BUFFER_DEFAULT_ROTATION_DISTANCE is called.
