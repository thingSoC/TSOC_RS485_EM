# TSOC_RS485_EM Theory of Operation

**TSOC_RS485_EM** is a ATMEGA328 based board with integrated RS485 driver, an Embedded Module for thingSoC.


The **TSOC_RS485_EM** connects any thingSoC or Mikrobus module to an RS485 compatible slave interface,
including a variety of analog sensors, such as Temperature, Wind, Pressure, Air Quality, and much more.
The **TSOC_RS485_EM** can be configured as either a thingSoC master module (female connectors), or a thingSoC slave module (male connectors),
which is implemented as an assembly/build time option.

[![thingSoC TSOC_RS485_EM](http://patternagents.github.io/img/projects/TSOC_RS485_EM/TSOC_RS485_EM_top.png)  
*TSOC_RS485_EM*](https://github.com/PatternAgents/TSOC_RS485_EM/)

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



### Page A : USB Connector, Battery Connector and Power Supply<a name="PAGEA"/>

Q1, a [FDC6420C](https://www.fairchildsemi.com/datasheets/FD/FDC6420C.pdf) , is a complementary (N-Channel and P-Channel) power MOSFET 
used to select between [USB Power](https://en.wikipedia.org/wiki/USB#USB_Power_Delivery) and an external 3.7 Volt single-cell 
[Li-Po battery](https://en.wikipedia.org/wiki/Lithium_polymer_battery) as the primary power input. 
[Resistor, R6 is used to "pull-down" the GATE of Q1P, turning it on, and enabling the battery (VBAT) to apply power to U2 (VIN).
If USB1 is connected and power is provided to USB1_VBUS, then Resistor R4 powers the GATE of Q1N, turning it on (and turning Q1P off...),
enabling USB1_VBUS to apply power to U2 (VIN).

U2, a [NCP361](http://www.onsemi.com/pub_link/Collateral/NCP361-D.PDF) , is a USB VBUS protection device, with an error output flag to indicate
an undervoltage, overvoltage, or overcurrent condition. The !5V0_FAULT (error flag) signal is active low, 
and is used to disable U5, the 3.3 Volt reulator. U5 a [MIC5219](http://www.micrel.com/_PDF/mic5219.pdf) Low DropOut Regulator (LDO),
is used to provide the 3.3 Volt power rail. The power protection scheme is much faster (5/1000 of a second) more efficient than chemical
or resetable fuses, such as the PPTC fuse normally used for USB power on the typical Arduino board.

U1, a [MCP73831](http://www.microchip.com/wwwproducts/en/en024903) , is a tiny 500mA linear battery charger, used to charge the battery when
USB1 is connected and power is provided to USB1_VBUS. Battery Charger U1 is only enabled after USB enumeration and ower arbitration by the 
BCD0 (Battery Charger Detect) signal, coming from the U4, the USB-UART interface device.

![Schematic Page A](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_1.png "Schematic Page A")

Limitations: 

1) The TSOC_RS485_EM is primarily a 3.3 Volt system, and not all pins are 5V tolerant. 

2) When using single cell Li-Po battery power, the 5V output power pin may be as low as 3.45 Volts,
   as there is no "boost" regulator circuitry included. If 5V power is needed for peripheral
   boards and sensors, it is suggested to use an external USB battery system instead of a single cell Li-Po battery.
   
   
### Page B : USB to UART Bridge Controller <a name="PAGEB"/>

U4, a [CY7C65213](http://www.cypress.com/file/139881/download), 
is an integrated USB-to-UART bridge device that provides the USB-to-UART
function with a minimal number of components.
[CY7C65213](http://www.cypress.com/file/139881/download), includes a USB 2.0 Full-Speed
controller, a UART transceiver, an internal regulator, an internal
oscillator, and a 512-byte flash in a 28-pin SSOP package.
The internal flash is used to store custom-specific USB
descriptors and GPIO configuration. This is done in-system
using a configuration utility that communicates over the USB
interface. The [CY7C65213](http://www.cypress.com/file/139881/download),
implements the USB2.1 BCD (Battery Charger Detect) protocol,
and only enabels the battery charger after USB enumeration is complete.

![Schematic Page B](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_2.png "Schematic Page B")

### Page C <a name="PAGEC"/>

![Schematic Page C](https://github.com/thingSoC/TSOC_RS485_EM/blob/master/TSOC_RS485_EM/docs/images/sch_page_3.png "Schematic Page C")

### Page D <a name="PAGED"/>

![Schematic Page D](https://raw.githubusercontent.com/PatternAgents/TSOC_RS485_EM/master/TSOC_RS485_EM/docs/images/sch_page_4.png "Schematic Page D")

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
 
