# Wireless IDs

####Microcontroller Types
ID | Value | Description
:------:|:----:|:--------------
31 | 18F452, 20MHz
32 | 18F4620, 20MHz
33 | 18F46K20, 40MHz
34 | 18F67K90, 40MHz
35 | EFM32WG990F256, 48MHz

####Data Collection Method
ID | Value | Description
:------:|:----:|:--------------
 1 | Log Only | Data is logged to the Node's internal memory to be downloaded later
 2 | Tx Only | Data is transmitted wirelessly over the air
 3 | Log & Tx | Data is both logged to the Node and transmitted over the air.


####Data Type
ID | Value | Description
:------:|:----:|:--------------
1 | `uint16` (bit-shifted) | value is multiplied by 2 (divide by 2 when receiving)
2 | `float` |
3 | `uint16` (12-bit resolution) |
4 | `uint32` |
7 | `uint16` (16-bit resolution) |

####Data Format
ID | Value | Description
:------:|:----:|:--------------
1 | `uint16` | no calibration will be applied
2 | `float` | cal coefficients will be applied

####Sampling Mode
ID | Value | Description
:------:|:----:|:--------------
1 | Sync | The Synchronized Sampling mode
2 | Sync Burst | The Synchronized Sampling, Burst mode
3 | Async | The Asynchronous Sampling mode (LDC)
4 | Armed Datalogging | The Armed Datalogging Sampling mode

####Sync Sampling Mode
ID | Value | Description
:------:|:----:|:--------------
29696 | Continuous | Data will be transmitted in standard non-burst synchronized sampling mode.
62976 | Burst | Data will be transmitted in a burst synchronized sampling mode.

####Default Mode
ID | Value | Description
:------:|:----:|:--------------
0 | Idle Mode | Idle state in which the Node can be communicated with normally (default)
1 | Async Sampling | Starts Async Sampling (LDC)
4 | Armed Datalogging | Starts datalogging (but with no timestamp).
5 | Sleep | Low-Power Sleep Mode (must be set to idle to communicate).
6 | Sync Sampling | Starts Sync Sampling (must hear a beacon to start sampling).

####Frequency
ID | Value | Description
:------:|:----:|:--------------
11 | Frequency 11 | 2.405 Ghz
12 | Frequency 12 | 2.410 Ghz
13 | Frequency 13 | 2.415 Ghz
14 | Frequency 14 | 2.420 Ghz
15 | Frequency 15 | 2.425 Ghz
16 | Frequency 16 | 2.430 Ghz
17 | Frequency 17 | 2.435 Ghz
18 | Frequency 18 | 2.440 Ghz
19 | Frequency 19 | 2.445 Ghz
20 | Frequency 20 | 2.450 Ghz
21 | Frequency 21 | 2.455 Ghz
22 | Frequency 22 | 2.460 Ghz
23 | Frequency 23 | 2.465 Ghz
24 | Frequency 24 | 2.470 Ghz
25 | Frequency 25 | 2.475 Ghz
26 | Frequency 26 | 2.480 Ghz

####Transmit Power
ID | Value | Description
:------:|:----:|:--------------
25619 | 16 dBm | 39 mw
25615 | 10 dBm | 10 mw
25611 | 5 dBm | 3 mw
25607 | 0 dBm | 1 mw

####Retransmission
ID | Value | Description
:------:|:----:|:--------------
0 | Off | Retransmission is turned off.
1 | On | Retransmission is turned on
2 | Disabled | Software only lock. Software should not attempt to enable Retransmission.

####Trigger Type
ID | Value | Description
:------:|:----:|:--------------
0 | User Init | The user started this datalogging session manually by sending a start sampling command.
1 | Ceiling | The trigger was caused by a ceiling event.
2 | Floor | The trigger was caused by a floor event.
3 | Ramp Up | The trigger was caused by a ramp-up event.
4 | Ramp Down | The trigger was caused by a ramp-down event.

####Cal Coefficients - Equation Type
ID | Value | Description
:------:|:----:|:--------------
0 | `y = x` | value = bits
4 | `y = mx + b`| value = (slope * bits) + offset

####Cal Coefficients - Unit
ID | Value | Description
:------:|:----:|:--------------
0	| unknown | no unit or unknown unit
1	| bits | raw bits
2	| Strain
3	| microStrain
4	| acceleration due to gravity
5	| meters per second squared
6	| volts
7	| milliVolts
8	| microVolts
9	| degrees Celsius
10	| Kelvin
11	| degrees Fahrenheit
12	| meters
13	| millimeters
14	| micrometers
15	| pound force
16	| Newtons
17	| kiloNewtons
18	| kilograms
19	| bar
20	| pounds per square inch
21	| atmospheric pressure
22	| millimeters of mercury
23	| Pascal
24	| megaPascal
25	| kiloPascal
26	| degrees
27	| degrees per second
28	| radians per second
29	| percent
30	| revolutions per minute
31	| hertz
32	| percent relative humidity
33	| milliVolt/Volt
34	| milli-G's
