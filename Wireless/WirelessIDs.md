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
