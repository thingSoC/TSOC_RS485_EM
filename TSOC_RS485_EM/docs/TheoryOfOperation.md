# TSOC_RS485_EM Theory of Operation

**TSOC_RS485_EM** is a ATMEGA328 based board with integrated RS485 driver, an Embedded Module for thingSoC.


The **TSOC_RS485_EM** connects any thingSoC or Mikrobus module to an RS485 compatible slave interface,
including a variety of analog sensors, such as Temperature, Wind, Pressure, Air Quality, and much more.
The **TSOC_RS485_EM** can be configured as either a thingSoC master module (female connectors), or a thingSoC slave module (male connectors),
which is implemented as an assembly/build time option.

---------------------------------------

[![thingSoC TSOC_RS485_EM](http://thingsoc.github.io/img/projects/TSOC_RS485_EM/TSOC_RS485_EM_top.png)  
*TSOC_RS485_EM*](https://github.com/thingSoC/TSOC_RS485_EM/)

* [thingSoC Compliant Module](http://www.thingsoc.com)
* [Mikrobus Compatible Module](http://www.mikroe.com/mikrobus/) 
* [Modbus](http://www.modbus.org/specs.php) Compliant Slave Interface
* [5 Volt](https://en.wikipedia.org/wiki/Modbus) Nominal Power Input with ESD and OV/OC protections
* Supports Six (6) Analog  Inputs  (ADC) 
* Supports Six (6) Digital Outputs (3.3V)
* Supports Six (2) Digital Inputs  (3.3V)
* Supports Remote I2C Interface
* Supports Remote UART Interface
* Supports Remote SPI Interface
* Easily add Modbus Interface support to any device or sensor, with little development time or experience

---------------------------------------

## Theory of Operation <a name="theory_index"/>



### Page A : ATMEGA328 Processor (Atmel AVR - Arduino Compatible)<a name="PAGEA"/>

The **TSOC_RS485_EM** can use either an ATMEGA328 or ATMEGA328P in a 32 PIN TQFP Package.

X1 is a Murata Resonator, typically populated with an 8MHz component (16 MHz by request).

![Schematic Page A](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_1.png "Schematic Page A")


### Page B : thingSoC Compliant Socket <a name="PAGEB"/>

The **TSOC_RS485_EM** incorporates a standard thingSoC Compliant socket pattern, and can be configured for either master or slave socket operation.

R17, R18, R19, R20, and R21 are used to swap transmit amnd receive, or to enable or disable external connections for D0, D1, and D2.
Normally D0, D1, and D2 are used for the RS-485 tranceiver, and so R17, R18, R19, R20, and R21 are DNP (Do Not Populate).


![Schematic Page B](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_2.png "Schematic Page B")

### Page C : Power Supply <a name="PAGEC"/>

Q1, a [FDC6420C](https://www.fairchildsemi.com/datasheets/FD/FDC6420C.pdf) , is a complementary (N-Channel and P-Channel) power MOSFET 
used to select between the internal TSOC socket power (slave operation), and the external 5V power supply (master operation).
Resistor, R15 is used to "pull-down" the GATE of Q1P, turning it on, and enabling the TSOC socket 5V to apply power to U4 (VIN).
If external 5V0 is connected, then Resistor R13 powers the GATE of Q1N, turning it on (and turning Q1P off...),
enabling external 5V0 to apply power to U4 (VIN).

U4, a [NCP361](http://www.onsemi.com/pub_link/Collateral/NCP361-D.PDF) , is a USB VBUS protection device, with an error output flag to indicate
an undervoltage, overvoltage, or overcurrent condition. The !5V0_FAULT (error flag) signal is active low, 
and is used to disable U3, the 3.3 Volt reulator. U3 a [MIC5219](http://www.micrel.com/_PDF/mic5219.pdf) Low DropOut Regulator (LDO),
is used to provide the 3.3 Volt power rail. The power protection scheme is much faster (5/1000 of a second) more efficient than chemical
or resetable fuses, such as the PPTC fuse normally used for USB power on the typical Arduino board.


![Schematic Page C](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_3.png "Schematic Page C")

### Page D : RS485 Tranceiver <a name="PAGED"/>

![Schematic Page D](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_4.png "Schematic Page D")

U1, an ST1480ACSOIC, is an RS-485 transceiver, capable of either 3.3V or 5V operation.

Solder Jumper, SJ3 is used to disconnect the onboard ST1480ACSOIC RS-485 transceiver,
and enables the use of an external driver for the main UART on D0 & D1.

Limitations: 

1) The **TSOC_RS485_EM** can use either 3.3V or 5V for VCC, either a 3.3V or 5V FTDI USB-UART can be used.

2) The **TSOC_RS485_EM** expects a 5.0V Volt external power supply input, do not exceed 5.0V power input (i.e. USB). 

 
---------------------------------------

## Jumper Settings <a name="jumpers"/>

* SJ1 - TSOC 3.3V Enable : Enables/Disables 3.3V power to an external thingSoC board. Default is enabled (connected).

* SJ2 - VCC 3,3V or 5.0V select, up for 5.0 Volt operation, down for 3.3 Volt operation. Default is 3.3V VCC (down).

* SJ3 - Internal RS-485 Driver Enable. Default is enabled (connected).

---------------------------------------

## Master/Slave Settings <a name="master_slave"/>

* MASTER - Using Onboard RS-485 Tranceiver, configure as follows:  
  SJ1 : Installed  
  SJ3 : Installed  
  R17, R18, R19, R20, R21 : Removed (not populated)  
  
* MASTER - disable Onboard RS-485 Tranceiver, configure as follows:  
  SJ1 : Installed  
  SJ3 : Removed  
  R17, R19, R21 : Installed (1K Ohms)  
  R18, R20 : Removed (not populated)  
  
* SLAVE - Using Onboard RS-485 Tranceiver, configure as follows:  
  SJ1 : Removed  
  SJ3 : Installed  
  R17, R18, R19, R20, R21 : Removed (not populated)  
  
* SLAVE - disable Onboard RS-485 Tranceiver, configure as follows:  
  SJ1 : Removed  
  SJ3 : Removed  
  R17, R18, R20 : Installed (1K Ohms)  
  R19, R21 : Removed (not populated)  

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
 
