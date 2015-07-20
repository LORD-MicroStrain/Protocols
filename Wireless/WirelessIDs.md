# Wireless IDs

####Microcontroller Types

The type of microcontroller on the device. `EEPROM 120`

ID | Value | Description
:------:|:----:|:--------------
31 | 18F452, 20MHz
32 | 18F4620, 20MHz
33 | 18F46K20, 40MHz
34 | 18F67K90, 40MHz
35 | EFM32WG990F256, 48MHz

####Data Collection Method

The data collection method when performing Sync or Async Sampling. `EEPROM 38`

ID | Value | Description
:------:|:----:|:--------------
 1 | Log Only | Data is logged to the Node's internal memory to be downloaded later
 2 | Tx Only | Data is transmitted wirelessly over the air
 3 | Log & Tx | Data is both logged to the Node and transmitted over the air.


####Data Type

The type of the data that is collected.

ID | Value | Description
:------:|:----:|:--------------
1 | `uint16` (bit-shifted) | value is multiplied by 2 (divide by 2 when receiving)
2 | `float` |
3 | `uint16` (12-bit resolution) |
4 | `uint32` |
7 | `uint16` (16-bit resolution) |

####Data Format

The type of data formats that can be applied to a Wireless Node. `EEPROM 76`

ID | Value | Description
:------:|:----:|:--------------
1 | `uint16` | no calibration will be applied
2 | `float` | cal coefficients will be applied

####Sampling Mode

The sampling mode that the device's configuration is applied for. `EEPROM 24`

ID | Value | Description
:------:|:----:|:--------------
1 | Sync | The Synchronized Sampling mode
2 | Sync Burst | The Synchronized Sampling, Burst mode
3 | Async | The Asynchronous Sampling mode (LDC)
4 | Armed Datalogging | The Armed Datalogging Sampling mode

####Sync Sampling Mode

The Sync Sampling mode that will be used when configured for Sync Sampling. `EEPROM 262`

ID | Value | Description
:------:|:----:|:--------------
29696 | Continuous | Data will be transmitted in standard non-burst synchronized sampling mode.
62976 | Burst | Data will be transmitted in a burst synchronized sampling mode.

####Default Mode

The mode a Wireless Node starts in, and goes into after a user inactivity timeout. `EEPROM 18`

ID | Value | Description
:------:|:----:|:--------------
0 | Idle Mode | Idle state in which the Node can be communicated with normally. (default)
1 | Async Sampling | Starts Async Sampling (LDC)
4 | Armed Datalogging | Starts datalogging (but with no timestamp).
5 | Sleep | Low-Power Sleep Mode (must be set to idle to communicate).
6 | Sync Sampling | Starts Sync Sampling (must hear a beacon to start sampling).

####Frequency

The Wireless Frequency of a device. `EEPROM 90`

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

The transmit power level. `EEPROM 94`

ID | Value | Description
:------:|:----:|:--------------
25619 | 16 dBm | 39 mw
25615 | 10 dBm | 10 mw
25611 | 5 dBm | 3 mw
25607 | 0 dBm | 1 mw

####Retransmission

Whether retransmission (used for lossless Sync Sampling) is on or off. `EEPROM 272`

ID | Value | Description
:------:|:----:|:--------------
0 | Off | Retransmission is turned off.
1 | On | Retransmission is turned on
2 | Disabled | Software only lock. Software should not attempt to enable Retransmission.

####Trigger Type

The type of a trigger that caused a datalogging session.

ID | Value | Description
:------:|:----:|:--------------
0 | User Init | The user started this datalogging session manually by sending a start sampling command.
1 | Ceiling | The trigger was caused by a ceiling event.
2 | Floor | The trigger was caused by a floor event.
3 | Ramp Up | The trigger was caused by a ramp-up event.
4 | Ramp Down | The trigger was caused by a ramp-down event.

####Cal Coefficients - Equation Type

The equation type for cal coefficients. `EEPROM 150 (ch1) - 220 (ch8)`

ID | Value | Description
:------:|:----:|:--------------
0 | `y = x` | value = bits
4 | `y = mx + b`| value = (slope * bits) + offset

####Cal Coefficients - Unit

The unit type foe cal coefficients. `EEPROM 150 (ch1) - 220 (ch8)`

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

####Settling Time

The settling time used for thermocouple and voltage inputs. `EEPROM 130 & 134`

ID | Value | Description
:------:|:----:|:--------------
1		| 4 ms | fastest settling
2		| 8 ms |
3		| 16 ms
4		| 32 ms
5		| 40 ms
6		| 48 ms
7		| 60 ms
8		| 101 ms | 90db [60Hz Rejection]
9		| 120 ms | 80db [50Hz Rejection]
10	| 120 millisecond settling time | 65db [50+60Hz Rejection]
11	| 160 millisecond settling time | 69db [50+60Hz Rejection]
12	| 200 millisecond settling time | highest resolution

####Thermocouple Type

The Thermocouple Type of a Wireless thermocouple channel. `EEPROM 306`

ID | Value | Description
:------:|:----:|:--------------
0		| Uncompensated | no thermocouple type
1		| K Type
2		| J Type
3		| R Type
4		| S Type
5		| T Type
6		| E Type
7		| B Type
8		| N Type
9		| Custom Polynomial

####Sample Rate

The Sample Rate (device and sampling mode dependent). `EEPROM 72`

ID | Value | Description
:------:|:----:|:--------------
60	| 104170 Hz 
58	| 78125 Hz
57	| 62500 Hz
56	| 25000 Hz
55	| 12500 Hz
49	| 3200 Hz
48	| 1600 Hz
47	| 800 Hz
62	| 1 kHz
63	| 2 kHz
64	| 3 kHz
65	| 4 kHz
66	| 5 kHz
67	| 6 kHz
68	| 7 kHz
69	| 8 kHz
70	| 9 kHz	
71	| 10 kHz
72	| 20 kHz
73	| 30 kHz
74	| 40 kHz
75	| 50 kHz
76	| 60 kHz
77	| 70 kHz
78	| 80 kHz
79	| 90 kHz
80	| 100 kHz
101	| 4096 Hz
102	| 2048 Hz
103	| 1024 Hz
104	| 512 Hz
105	| 256 Hz
106	| 128 Hz
107	| 64 Hz
108	| 32 Hz
109	| 16 Hz
110	| 8 Hz
111	| 4 Hz
112	| 2 Hz
113	| 1 Hz
114	| 1 sample every 2 seconds
115	| 1 sample every 5 seconds
116	| 1 sample every 10 seconds
117	| 1 sample every 30 seconds
118	| 1 sample every 1 minute
119	| 1 sample every 2 minutes
120	| 1 sample every 5 minutes
121	| 1 sample every 10 minutes
122	| 1 sample every 30 minutes
123	| 1 sample every 60 minutes
127	| 1 sample every 24 hours
