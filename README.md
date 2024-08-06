This repository is a fork of [esphome-standing-desk](https://github.com/tjhorner/esphome-standing-desk) by @tjhorner.
At the same time it merges the adoptions [DanielHabenicht / logicdata-standing-desk](https://github.com/DanielHabenicht/logicdata-standing-desk/tree/main) to have functionality for Logicdata desk - but ended up not using it at the moment (read below). 

This fork/merger was created to make it compatible with latest ESPHome Version. 
Within further deep dive into the topic I had to experience, that the configuration by @DanielHabenicht wouldn't function properly on my desk: 
- current height was not measured (sensor had no value)
- up button moved desk up, but not to the highest level
- save button wouldn't save any position, but instead moved the desk up to it's maximum level
- memory position 4 was without any function

So I thought I messed up with the wiring and re-measured the voltage for the 7 Pins on the connector and so on. But everything was correct. Then I dived deeper into to provided records from SeaLogicAnalyzer but I ended up realizing that if somethings messed up I wouldn't be able to find the correct way with the given information. 

So I started to give 5 Volts to the pins manually and noticed, that you can address the basic functions of the logicdata control unit quite simple. For me this is: 
Up, Down, Memory1 and Memory2. Personally I don't need more than this. 

In the future I will probably work to get the "current height" sensor working in Order to send a specific height. Furthermore the save button would be great - but at the moment it's fine for me.  

First of all the Layout of the 7-Pin-Din connector:

![7-Pin-Din connector](https://github.com/RoMaTiX99/esphome-standing-desk/blob/master/LOGICDATA_7-PIN_Connector_Handset.png)


Here's what worked for me: 
| Line  | Description                                  | Colours          | ESP32 Pin |
| ----- | -------------------------------------------- | ---------------- |-----------|
| SHELL | Ground                                       | Grey             | GND       |
| 1     | up                                           | white            | GPIO16    |
| 5     | Memory Position 1                            | blue             | GPIO17    |
| 2     | Memory Position 2                            | green            | GPIO18    |
| 4     | down                                         | yellow           | GPIO19    |


So the following three Pins / cables don't need to be connected for basic functionality (up/down/mem1/mem2):
| Line  | Description                                  | Colours          | ESP32 Pin |
| ----- | -------------------------------------------- | ---------------- |-----------|
| 3     |                                              | brown            | -         |
| 6     |                                              | red              | -         |
| 7     |                                              | black            | -         |

I used 7-Pin-DIN Y-Splitter-Cable from here: [Aliexpress](https://de.aliexpress.com/item/1005003269764721.html?spm=a2g0o.order_list.order_list_main.5.61e95c5fDRpzA4&gatewayAdapt=glo2deu).
I ordered two of them and cut one on the female end and connected the wires to and ESP32. 

