Selected parts
==============

problems:
--------
- selected rpi2040 board only shares 6 free pins, which suggests to use I<sup>2</sup>C protocol for as many features as possible (2 additionall are available - 4 and 5, however they aren't on designated header)
- there is no configuration, where we can use SPI0 on second board because of the pins that were selected to be free, SPI1 is used for display
- second board needs 3.3V power, and designated header doesn't provide actual 3.3V regulated power line





Free pins
=========

| pin num | spi option                  | I<sup>2</sup>C option                   |  UART option  |  selected purpose
|---------|------------                 | ----------------------                  |  ------------ | ----------
|  16     |SPI0 RX                      | **I<sup>2</sup>C0 SDA**                 |  UART0 TX     | **I<sup>2</sup>C0 SDA** 
|  17     |SPI0 CSn                     | **I<sup>2</sup>C0 SCL**                 |  UART0 RX     | **I<sup>2</sup>C0 SCL**
|  18     |SPI0 SCK                     | <strike>I<sup>2</sup>C1 SDA </strike>   |  UART0 CTS    | 
|  26     |<strike>SPI1 SCK</strike>    | <strike>I<sup>2</sup>C1 SDA </strike>   |  UART1 CTS    | 
|  27     |<strike>SPI1 TX </strike>    | <strike>I<sup>2</sup>C1 SCL </strike>   |  UART1 RTS    | 
|  28     |<strike>SPI1 RX </strike>    | I<sup>2</sup>C0 SDA                     |  UART0 TX     | 
|   4     |SPI0 RX                      | I<sup>2</sup>C0 SDA                     |  UART1 TX     | 
|   5     |SPI0 CSn                     | I<sup>2</sup>C0 SCL                     |  **UART1 RX** | **UART1 RX** for GPS

I<sup>2</sup>C1 is used onboard for IMU

SPI1 is used for the display, SPI0 has no available TX pin on free pins from the watch module

This probably means, that SD card has to be bitbanged to selected (in near future) pins (**bad idea**), or we need to use PIO in order to exchange data throug SPI **with adequate throughput**


I<sup>2</sup>C devices
======================

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



GPIO expander pins
==================

| expander pin num      | in/out      | purpose
| ----------------------| ------------| -------
| 0                     |     in      |  button0
| 1                     |     in      |  button1     
| 2                     |     in      |  button2     
| 3                     |             |        
| 4                     |             |        
| 5                     |             |        
| 6                     |     out     | SPI CS for SD       
| 7                     |     out     | GPS power control      
