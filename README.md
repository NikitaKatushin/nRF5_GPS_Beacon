# nRF5_GPS_Beacon

Scope:
The scope of this document is to describe the logic and maintenance of the program. 
This document has to be followed to ensure proper use and functionality of the beacon. 
For the following task ble_app_uart project was used as a template. 
Segger Embedded System IDE was used for developing.

Description:
The following program works as UART/Bluetooth transmitter/receiver. The user can enter GPS coordinates (latitude and longitude). 
The coordinates are sent via UART communication protocol(*). Therefore, any terminal emulator that connects COM port can be used. 
The coordinates are sent in format SXX.YY, where S is sign (can be +/-), XX are decimals and YY are float numbers. 
The program approves that numbers are sent in proper boundaries. The longitude can be sent in range -90.0/+90.0 and and the longitude in range -180.0/+180.0. 
The terminal will prompt an error in case wrong numbers are entered. After that the data are needed to be set again(for current type of geographic coordinate). 
If boundaries are fulfilled, the data is coded(**) and can be sent over bluetooth. In order to validate received advertising data the nRF Connect tool can be used. 
The name of the development board is “GPS_NRF5_BEACON”. The received data is sent in the following format: XXXYYXXXYY(Note that no commas are sent). 
An example set of operands and the correct result are shown below: 

Latitude: (45.36 + 360) * 100 = 40536
Longitude: (120.12 + 360) * 100 = 48012
Received data package: 4053648012

The data can be decoded using the opposite procedure.


(*)UART baudrate is 9600

(**)Float data types cannot be sent over bluetooth, which means coding/decoding procedure. The entered value is added 360 and multiplied by 100. Afterwards it cast each digit to uint8_t data array. 

Setup:
In order to open the project you need to have nRF5_SDK_15.3.0. Download the repository and unzip it to the following direction: ...\nRF5_SDK_15.3.0_59ac345\examples\ble_peripheral

You can open the project from:
...\nRF5_SDK_15.3.0_59ac345\examples\ble_peripheral\nRF5_GPS_Beacon\pca10040\s132\ses\ble_app_uart_pca10040_s132
