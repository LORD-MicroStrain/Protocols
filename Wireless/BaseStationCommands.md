# Base Station Commands


## Ping Base Station

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x01    | 0         | uint8  | Command ID

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x01    | 0         | uint8  | Command ID

<br>
## Read Base Station EEPROM

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  See the Base Station EEPROM Map for specific memory address details.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x73    | 0         | uint8  | Command ID
0xXXXX  | (1 - 2)   | uint16 | EEPROM address to read
0xXXXX  | 3         | uint16 | Checksum (1 - 2)

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x73    | 0         | uint8  | Command ID
0xXXXX  | (1 - 2)   | uint16 | Value read from EEPROM
0xXXXX  | 3         | uint16 | Checksum (1 - 2)

##### Fail Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x21    | 0         | uint8  | Fail ID

<br>
## Write Base Station EEPROM

The **Write Base Station EEPROM** command is used to write a value to a specific memory address on the Base Station's EEPROM.

See the Base Station EEPROM Map for specific memory address details.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x78    | 0         | uint8  | Command ID
0xXXXX  | (1 - 2)   | uint16 | EEPROM address to write to
0xXXXX  | (3 - 4)   | uint16 | Value to write to EEPROM
0xXXXX  | 5         | uint16 | Checksum (1 - 4)

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x78    | 0         | uint8  | Command ID
0xXXXX  | (1 - 2)   | uint16 | Value written to EEPROM
0xXXXX  | 3         | uint16 | Checksum (1 - 2)

##### Fail Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x21    | 0         | uint8  | Fail ID


<br>
## Enable Beacon

The Enable Beacon command is used to turn on the beacon on the Base Station.<br>
The beacon is used to synchronize and start a group of nodes when performing Synchronized Sampling.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0xBEAC  | (0 - 1)   | uint16 | Command ID
0xXXXXXXXX  | (2 - 5)   | uint32 | Timestamp to give to the Beacon

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0xBEAC  | (0 - 1)   | uint16 | Command ID

##### Fail Response:
None.

##### Notes:
**Command Packet Timestamp**: The last 4 bytes in the Command Packet are Timestamp bytes. The beacon that is started from this command will send a Timestamp beginning from this value. These bytes represent the current UTC time in seconds from the Unix Epoch (January 1, 1970). 


<br>
## Disable Beacon

The Disable Beacon command is used to turn off the beacon on the Base Station. Sending the Stop Node command from the Base Station that is beaconing will automatically turn off the beacon as well.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0xBEAC  | (0 - 1)   | uint16 | Command ID
0xFFFFFFFF  | (2 - 5)   | uint32 | Disable Beacon Value

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0xBEAC  | (0 - 1)   | uint16 | Command ID

##### Fail Response:
None.

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.
