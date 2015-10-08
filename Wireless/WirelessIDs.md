# Wireless IDs

####Microcontroller Types 
`EEPROM 120` | `BaseStation` | `Node`

The type of microcontroller on the device.

ID | Value | Description
:------:|:----:|:--------------
31 | 18F452, 20MHz
32 | 18F4620, 20MHz
33 | 18F46K20, 40MHz
34 | 18F67K90, 40MHz
35 | EFM32WG990F256, 48MHz

####Data Collection Method
`EEPROM 38` | `Node`

The data collection method when performing Sync or Async Sampling.

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
`EEPROM 76` | `Node`

The type of data formats that can be applied to a Wireless Node.

ID | Value | Description
:------:|:----:|:--------------
1 | `uint16` | no calibration will be applied
2 | `float` | cal coefficients will be applied

####Sampling Mode
`EEPROM 24` | `Node`

The sampling mode that the device's configuration is applied for.

ID | Value | Description
:------:|:----:|:--------------
1 | Sync | The Synchronized Sampling mode
2 | Sync Burst | The Synchronized Sampling, Burst mode
3 | Async | The Asynchronous Sampling mode (LDC)
4 | Armed Datalogging | The Armed Datalogging Sampling mode

####Sync Sampling Mode
`EEPROM 262` | `Node`

The Sync Sampling mode that will be used when configured for Sync Sampling.

ID | Value | Description
:------:|:----:|:--------------
29696 | Continuous | Data will be transmitted in standard non-burst synchronized sampling mode.
62976 | Burst | Data will be transmitted in a burst synchronized sampling mode.

####Default Mode
`EEPROM 18` | `Node`

The mode a Wireless Node starts in, and goes into after a user inactivity timeout.

ID | Value | Description
:------:|:----:|:--------------
0 | Idle Mode | Idle state in which the Node can be communicated with normally. (default)
1 | Async Sampling | Starts Async Sampling (LDC)
4 | Armed Datalogging | Starts datalogging (but with no timestamp).
5 | Sleep | Low-Power Sleep Mode (must be set to idle to communicate).
6 | Sync Sampling | Starts Sync Sampling (must hear a beacon to start sampling).

####Frequency
`EEPROM 90` | `BaseStation` | `Node`

The Wireless Frequency of a device.

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
`EEPROM 94` | `BaseStation` | `Node`

The transmit power level.

For Nodes with FW >= 10.0 and BaseStations with FW >= 4.0:

ID | Value | Description
:------:|:----:|:--------------
20 | 20 dBm | 100 mw
16 | 16 dBm | 39 mw
10 | 10 dBm | 10 mw
5 | 5 dBm | 3 mw
0 | 0 dBm | 1 mw

For Nodes with FW < 10.0 and BaseStations with FW < 4.0:

ID | Value | Description
:------:|:----:|:--------------
25619 | 16 dBm | 39 mw
25615 | 10 dBm | 10 mw
25611 | 5 dBm | 3 mw
25607 | 0 dBm | 1 mw

####Retransmission
`EEPROM 272` | `Node`

Whether retransmission (used for lossless Sync Sampling) is on or off.

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

####Settling Time
`EEPROM 130 & 134` | `Node`

The settling time used for thermocouple and voltage inputs.

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
`EEPROM 306` | `Node`

The Thermocouple Type of a Wireless thermocouple channel.

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
`EEPROM 72` | `Node`

The Sample Rate (device and sampling mode dependent).

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

####Region Code
`EEPROM 280` | `BaseStation` | `Node`

The region that the device will be operated in.

ID | Value | Description
:------:|:----:|:--------------
0	| USA
1	| Europe
2| Japan
3	| Other
4	| Brazil

####LED Action
`EEPROM 238` | `BaseStation`

A bitmask control of the LED on the BaseStation:

Bit # | Description
:------:|:----
1	| Green LED - Default, Power On 
2	| Blue LED - Beacon Transmission indicator (from the device)
3 | Red LED - Alternate Beacon Reception indicator (to the device)

####Beacon Source
`EEPROM 96` | `BaseStation`

The source of a Base Station's beacon.

ID | Value | Description
:------:|:----:|:--------------
0 | None | No Beacon
1 | Internal Timer 
2 | Internal PPS
3 | External PPS

####PPS Edge Detection
`EEPROM 100` | `BaseStation`

**Internal Use**

Tells the microcontroller which edge to interrupt off of when using a PPS for timing.

**For BaseStation FW >= 4.0** :

ID | Value | Description
:------:|:----:|:--------------
0 | Off
1 | Rising Edge 
2 | Falling Edge
3 | Rising and Falling Edge

**For BaseStation FW < 4.0** :

ID | Value | Description
:------:|:----:|:--------------
0 | Falling Edge
1 | Rising Edge 

####Button Actions
`EEPROMs 232, 236, 258, 262` | `BaseStation`

The actions that can be performed by a Base Station's physical buttons. 

ID | Value | Description
:------:|:----:|:--------------
0 | Node Sleep | Puts a Node into sleep mode.
1 | Node Set to Idle | Puts a Node into idle mode.
2 | Enable Beacon | Enable the Base Station's beacon.
3 | Disable Beacon | Disables the Base Station's beacon.
4 | Start Node Non-Sync Sampling | Starts a Node sampling in Non-Sync mode.
5 | Start Node Sync Sampling | Starts a Node sampling in Sync mode.
6 | Start Node Armed Datalogging | Starts a Node sampling in Armed Datalogging mode.
7 | Cycle Power | Cycles the Base Station's power.
65535 | Disabled | Disables the button functionality.

####Firmware Version
`EEPROM 108 and 110` | `BaseStation` | `Node`

The firmware version of the device.

**For BaseStation FW >= 4.0 and Node FW >= 10.0** :
The firmware version of Base Stations and Wireless Nodes are repesented in the following format: `Major.Revision`
where `Major` is the first byte (MSB) of EEPROM 108, and `Revision` is a 3 byte value created by combining the last byte (LSB) of EEPROM 108 and both bytes of EEPROM 110.

For example:

```cpp
uint16_t fwValue1 = readEeprom(108);
uint16_t fwValue2 = readEeprom(110);

uint8_t msb1 = fwValue1 >> 8;
uint8_t lsb1 = fwValue1 & 0x00FF;
uint8_t msb2 = fwValue2 >> 8;
uint8_t lsb2 = fwValue2 & 0x00FF;

uint16_t hiWord = (0 << 8) | lsb1;
uint16_t loWord = (msb2 << 8) | lsb2;

uint8_t major = msb1;
uint32_t revision = static_cast<uint32_t>(hiWord) << 16 | static_cast<uint32_t>(loWord)
```

**For BaseStation FW < 4.0 and Node FW < 10.0** (LEGACY):
The firmware version of Base Stations and Wireless Nodes are repesented in the following format: `Major.Minor`
where `Major` is the first byte (MSB) of EEPROM 108, and `Minor` is the last byte (LSB) of EEPROM 108.

For example:

```cpp
uint16_t fwValue = readEeprom(108);

uint8_t major = fwValue >> 8;
uint8_t minor = fwValue & 0x00FF;
```

####Channel Mask
`EEPROM 12` | `Node`

The Wireless Nodes use a channel mask to determine which channels are active and inactive on the device. 

Channels that are active will be sampled during any type of sampling mode. The mask is a 16-bit value. Each of the 16 bits of the mask correspone to one of the Node's channels (if that Node supports that channel). Bit 1 correpsonds to channel 1, bit 2 to channel 2, bit 8 to channel 8, etc. When the bit is set to 1, the channel is active. When the bit is set to 0, the channel is inactive.

For example:

```cpp
uint16_t ch1_ch6 = 33;   //0000 0000 0010 0001 (Channel 1 and Channel 6 enabled)

uint16_t ch3thru8 = 252; //0000 0000 1111 1100 (Channel 3 through 8 enabled)
```

####Sampling Delay
`EEPROM 34` | `Node`

The sampling delay sets the duration (in milliseconds) of pulsed power sensor excitation i.e. the amount of time between sensor excitation power up and A/D sampling.  Low-impedance sensors with slow rise times can exhibit longer settling time, and thus benefit from a larger delay before sampling.  Smaller delay values reduce power consumption during LDC. Note that this value only applies to sample rates less than 32 Hz, since sensor excitation power is applied full time for sample rates of 32 Hz and above. A value of 10,000 may be entered into this location to provide full time excitation power for sample rates below 32 Hz.

####Set to Idle Interval
`EEPROM 66` | `Node`

How often the Node wakes up and listens for a 'set to idle' command.

The following equation can be used to determine the specific value needed for a wake interval defined in seconds:

`Value = (7680 / Desired_Interval_in_seconds)`

For example, if the user wants the node to check for a wake command every 10 seconds, then this location would be programmed with a value of `(7680/10) = 768`.

The minimum wake interval is internally limited to 1 second (a value of `7680`), and the maximum wake interval is limited to approximately 15 seconds (a value of `512`). Any values outside of this range will be automatically truncated.  

NOTE: After modifying this value, the node must be reset in order for the changes to take effect.

####Calibration Coefficients
`EEPROM 150 - EEPROM 226` | `Node`

Calibration Coefficients are linear scaling filters applied to convert a channel's raw bit value to physical or engineering units. Please see the individual Node's hardware manual for more information on general calibration procedures. 

**Note**: The calibration coefficients slope and offset is different from a Node's hardware gain and offset settings.

**Note**: When a Node is transmitting 2-byte integer, uncalibrated values, Calibration Coefficients represent a post-processing step. The conversion from bits to physical units needs to take place after the data is received, and not on the Node. However, when the Node is transmitting 4-byte float, calibrated value, the conversion will occur on the Node and the received data values will already have been converted.

Each Channel requies 10 bytes to hold the equation, unit, slope, and offset values:

Description | type 
:------:|:----:
Equation ID | `uint8`
Unit ID | `uint8`
Slope | `float`
Offset | `float`

####Cal Coefficients - Equation Type
`EEPROM 150 (ch1) - EEPROM 220 (ch8)` | `Node`

The equation type for cal coefficients.

ID | Value | Description
:------:|:----:|:--------------
0 | `y = x` | value = bits
4 | `y = mx + b`| value = (slope * bits) + offset

####Cal Coefficients - Unit
`EEPROM 150 (ch1) - EEPROM 220 (ch8)` | `Node`

The unit type for cal coefficients.

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
