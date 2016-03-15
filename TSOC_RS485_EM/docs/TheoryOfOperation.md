# TSOC_RS485_EM Theory of Operation

**TSOC_RS485_EM** is a ATMEGA328 based board with integrated RS485 driver, an Embedded Module for thingSoC.


The **TSOC_RS485_EM** connects any thingSoC or Mikrobus module to an RS485 compatible slave interface,
including a variety of analog sensors, such as Temperature, Wind, Pressure, Air Quality, and much more.
The **TSOC_RS485_EM** can be configured as either a thingSoC master module (female connectors), or a thingSoC slave module (male connectors),
which is implemented as an assembly/build time option.

---------------------------------------

[![thingSoC TSOC_RS485_EM](http://thingsoc.github.io/img/projects/TSOC_RS485_EM/TSOC_RS485_EM_top.png)  
*TSOC_RS485_EM*](https://github.com/PatternAgents/TSOC_RS485_EM/)

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
used to select between [USB Power](https://en.wikipedia.org/wiki/USB#USB_Power_Delivery) and an external 3.7 Volt single-cell 
[Li-Po battery](https://en.wikipedia.org/wiki/Lithium_polymer_battery) as the primary power input. 
[Resistor, R6 is used to "pull-down" the GATE of Q1P, turning it on, and enabling the battery (VBAT) to apply power to U2 (VIN).
If USB1 is connected and power is provided to USB1_VBUS, then Resistor R4 powers the GATE of Q1N, turning it on (and turning Q1P off...),
enabling USB1_VBUS to apply power to U2 (VIN).

U4, a [NCP361](http://www.onsemi.com/pub_link/Collateral/NCP361-D.PDF) , is a USB VBUS protection device, with an error output flag to indicate
an undervoltage, overvoltage, or overcurrent condition. The !5V0_FAULT (error flag) signal is active low, 
and is used to disable U3, the 3.3 Volt reulator. U3 a [MIC5219](http://www.micrel.com/_PDF/mic5219.pdf) Low DropOut Regulator (LDO),
is used to provide the 3.3 Volt power rail. The power protection scheme is much faster (5/1000 of a second) more efficient than chemical
or resetable fuses, such as the PPTC fuse normally used for USB power on the typical Arduino board.


![Schematic Page C](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_3.png "Schematic Page C")

### Page D : RS485 Tranceiver <a name="PAGED"/>

![Schematic Page D](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_4.png "Schematic Page D")

Limitations: 

1) The TSOC_RS485_EM expects a 5.0V Volt power supply input, and can use either 3.3V or 5V for VCC. 

2) When using single cell Li-Po battery power, the 5V output power pin may be as low as 3.45 Volts,
   as there is no "boost" regulator circuitry included. If 5V power is needed for peripheral
   boards and sensors, it is suggested to use an external USB battery system instead of a single cell Li-Po battery.
   
   
   
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
 
