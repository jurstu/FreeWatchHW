Selected parts
==============

problems
--------
selected rpi2040 board only shares 6 free pins, which suggests to use I<sup>2</sup>C protocol for as many features as possible



| I<sup>2</sup>C device | model       | address
| --------------------- | ----------- | -------
| pulseoximeter         | MAX30102    | 0xAE
| RTC                   | DS3231      | 0x68
| GPIO expander         | MCP23009    | 0x20 - 0x27
| Gesture/light sensor  | APDS-9960   | 0x39
| magnetometer/compass  | idk yet     | idk yet


This leaves following features to be handled:    
- GPS module (1 pin for serial data)
- side buttons (0 pins since we have GPIO expander)
- SD card (3 pins for SPI and 1 pin from expander)
- bluetooth/wifi module (?)


It would also be nice to be able to turn the GPS module on/off from code using a mosfet or something (1 pin of expander)