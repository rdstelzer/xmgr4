
===================================================================
Stationery for the MCF5271 Freescale Board
===================================================================

Contents:

I)     Overview
II)    Files
III)   Memory maps
IV)    Initialization files
V)     Targets
VI)    Connecting to the board
VII)   Update the support folder
VIII)  Terminal Settings
IX)    Switch SW4 settings:


===================================================================
I)  Overview
===================================================================

This stationery is configured to run with the M5271EVB which contains
a MCF5271 product.

Here is a summary of what optional features exist within each 
product of the family:

Product        Ethernet    Encryption   USB
MCF5271           x             X        X

For more details, refer to the MCF523x Reference Manual

===================================================================
II)  Files
===================================================================

M5271_C.mcp - the project file

*.cfg - initialization files
*.mem - memory configuration file
*.lcf - linker configurations

src\console - main source for the M5235 Console Debug target
src\common  - common files used by all targets
src\include - All include files.

support\config - confugration files
support\include - harware specific header file
support\src - harware specific sorce file

obj\ - folder where all ELF and S-Record files are created

lcf\ - all lcf files

===================================================================
III)  Memory maps
===================================================================

All targets use the same basic memory map. Each target links code
and data sections into different RAM or ROM areas.

0x0000_0000 - 0x00FF_FFFF 16 Mbyte SDRAM
0x2000_0000 - 0x2000_FFFF 64 Kbytes Internal SRAM
0x3000_0000 - 0x300F_FFFF External ASRAM (not fitted)
0xFFE0_0000 - 0xFFFF_FFFF 2 Mbytes External Flash (U10)
or			  or
0xFFC0_0000 - 0xFFFF_FFFF 4 Mbytes External Flash (U11)

===================================================================
IV)  Initialization files
===================================================================

All initialization files setup the same memory map. The only
difference is the location of the VBR register at download time.

The P&E Protocol plugin allows the use of the "+-" panel
to capture various exceptions. After the code is downloaded, the
plugin attempts to overwrite the vector table entries and install its
own handler at locations VBR+0x408-0x40B to capture those selected
exceptions.  See descirption under Targets below.

m5271evb_pne.cfg - used in the M5271 RAM-CONSOLE Debug target.
m5271evb_pne.cfg - used in the M5271 RAM-UART Debug target.
m5271evb_pne.cfg - used in the M5271 ROM-UART Debug target.

===================================================================
V)  Targets
===================================================================

1) RAM-CONSOLE

This is the very basic stationery that outputs to the CodeWarrior's
console window.

Initialization file: m5271evb_pne.cfg

2) RAM-UART

This is the very basic stationery that outputs to the UART.
User need to connect the terminal to see the output.

Initialization file: m5271evb_pne.cfg

3) ROM-UART
This progrma copies the data from ROM to SDRAM
This is the very basic stationery that outputs to the UART.
User need to connect the terminal to see the output.

Initialization file: m5271evb_pne.cfg


===================================================================
VI)  Connection to the M5271EVB board
===================================================================

1) All jumper settings and switches are in their default locations
as outlined by the EVB user's manual.

2) The P&E cable is attached to the BDM connector.

3) An appropriate power supply is connected to p1 as outlined in the
EVB user's manual.

4) Check all the target Remote Connection panels to make sure the P&E
cable is selected.

===================================================================
VII) Update the support folder
===================================================================
In case any update in the init code then the support folder also
need an updated. You get the code from the Freescale site. Update
the support\include folder with all the relevant header files. Put
the necessary changes in the hwinit.c file from the sysinit.c file.

===================================================================
VIII)  Terminal Settings
===================================================================
The baud rate to be : 19200
Data bits : 8
Parity : None
Stop Bits : 1
Flow Control : None

===================================================================
IX)    Switch SW4 settings:
===================================================================

For Flash programming: 		 All On except SW4-4 = SW4-7 = OFF
For Debugging in External SDRAM: All On except SW4-4 = SW4-7 = OFF
For Debugging in External Flash: All On except SW4-4 = SW4-7 = OFF
