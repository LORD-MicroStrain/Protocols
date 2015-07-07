# Base Station Commands


### Ping Base Station

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x01    | 0         | uint8  | Command ID

##### Success Response:
Value   | Index     | Type   | Description
:------:|:---------:|:------:|:------------
0x01    | 0         | uint8  | Command ID

=====

### Read Base Station EEPROM

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

=====

### Write Base Station EEPROM

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
