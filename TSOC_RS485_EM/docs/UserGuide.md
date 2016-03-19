# TSOC_RS485_EM User Guide

**TSOC_RS485_EM** is a ATMEGA328 based board with integrated RS485 driver, an Embedded Module for thingSoC.


The **TSOC_RS485_EM** connects any thingSoC or Mikrobus module to an RS485 compatible slave interface,
including a variety of analog sensors, such as Temperature, Wind, Pressure, Air Quality, and much more.
The **TSOC_RS485_EM** can be configured as either a thingSoC master module (female connectors), or a thingSoC slave module (male connectors),
which is implemented as an assembly/build time option.

---------------------------------------

## User Guide <a name="userguide_index"/>


[![thingSoC TSOC_RS485_EM](http://thingSoC.github.io/img/projects/TSOC_RS485_EM/TSOC_RS485_EM_top.png)  
*TSOC_RS485_EM*](https://github.com/thingSoC/TSOC_RS485_EM/)

## Overview

The **TSOC_RS485_EM** is software/firmware compatible with a standard Arduino-Pro model,
employing the same ATMEL ATMEGA328 Microcontroller and the OptiBoot bootloader.
While any AVR development tools (i.e. Atmel Studio, etc.) may be used with the **TSOC_RS485_EM**,
this guide is primarily intended for use with the [Arduino IDE](https://www.arduino.cc/en/Main/Software) from [Arduino.cc](https://www.arduino.cc/).
The included files in the "examples" directory, are Arduino programs, known as "sketches", and using the .ino filename suffix.

## Why RS-485?

[RS-485](https://en.wikipedia.org/wiki/RS-485) is an older TIA/EIA standard for balanced digital multipoint, or "multi-drop" systems.
Examples of [RS-485](https://en.wikipedia.org/wiki/RS-485) based systems include theatre lighting (DMX/RDM512), 
early networking (Apple Talk), industrial process control (Modbus), vending machine bus control (VMB), and many other protocols and applications. 
The **TSOC_RS485_EM** is a simple and flexbile bridge tool for connecting a variety of other devices (sensors, relays, lights),
as well as other communications protocols (Ethernet, Wi-Fi, Bluetooth, etc) using [RS-485](https://en.wikipedia.org/wiki/RS-485).

## Why thingSoC?

[thingSoC](http://thingSoC.github.io) is an open source standard that defines a vendor independent socket system 
for the creation of new Internet Things; it addresses many of the limitations of current product offerings and standards, 
by adding capabilities such as automatic device discovery, device configuration, monitoring, instrumentation, and testing.

## TSOC_RS485_EM Compliance & Compatibility

The **TSOC_RS485_EM** is a [thingSoC](http://thingSoC.github.io) Compliant Module, and implements the [thingSoC Standard Embedded Module Format](http://thingSoC.github.io),
which defines the physical size, connector locations, mounting hole locations, as well as the automatic device discovery, device configuration, monitoring, instrumentation, 
and testing protocols. 

The **TSOC_RS485_EM** is also [MikroBus](http://www.mikroe.com/mikrobus/) compatible in most situations (depending on the pinout of the specific Mikrobus Module), 
and can use the majority of [Click](http://www.mikroe.com/click/) modules, available from [MikroElectronika](http://www.mikroe.com/). 
[MikroBus](http://www.mikroe.com/mikrobus/) and [Click](http://www.mikroe.com/click/) are registered tradmarks of [MikroElectronika](http://www.mikroe.com/).
We're busy doing interoperability testing using a variety of the [Click](http://www.mikroe.com/click/) modules with [thingSoC](http://thingSoC.github.io) modules,
and will be adding those as examples, as they are tested and verified. The [MikroElectronika](http://www.mikroe.com/) [Click](http://www.mikroe.com/click/) modules are inexpensive, 
and available from a number of [distributors](http://www.mikroe.com/distributors/) worldwide, and they are a good compliment to the unique features available
with [thingSoC](http://thingSoC.github.io) modules; however unlike [thingSoC](http://thingSoC.github.io) modules, the [Click](http://www.mikroe.com/click/) modules
do not include the automatic device discovery, device configuration, monitoring, instrumentation, features available with [thingSoC](http://thingSoC.github.io) modules.

## Examples

From the Arduino IDE, select File -> Examples -> TSOC_RS485_EM -> (example)

1) Blinky       :  Blinks the onboard Red, Green, Blue, and Yellow LEDs in sequence

2) DMX Master   :  Transmits a "fade-up" in brightness on DMX Channels 12 - 17

3) DMX Slave    :  Receive commands on DMX Channels 12-17  
  (12=Red, 13=Green, 14=Blue 15=Yellow, 16=Relay1, 17=Relay2)

4) Modbus Slave :  Receive commands on Modbus Address 1  
  (Holding Registers map to EEPROM, Coils to GPIO/Relays, etc.)


---------------------------------------

## Documentation Index <a name="documentation_index"/>

[TSOC_RS485_EM Quick Start Guide](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/QuickStart.md)

[TSOC_RS485_EM User Guide](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/UserGuide.md)

[TSOC_RS485_EM Theory of Operation](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/TheoryOfOperation.md)

[thingSoC Organization Website](http://thingSoC.github.io)

[thingSoC FAQ - Frequently Asked Questions](http://thingsoc.github.io/support/faq.html)

[ESP8266 Community](https://github.com/esp8266/Arduino)

---------------------------------------

[![Image](http://thingsoc.github.io/img/projects/thingSoC/thingSoC_thumb.png?raw=true)  
*thingSoC*](http://thingsoc.github.io) 
 
