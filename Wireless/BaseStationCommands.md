# Base Station Commands


### Ping Base Station

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
Value | # Bytes | Type | Description
------|---------|------|------------
0x01  | 1       | uint8 | Command ID

##### Success Response:
Value | # Bytes | Type | Description
------|---------|------|------------
0x01  | 1       | uint8 | Command ID

=====

### Read Base Station EEPROM

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station’s EEPROM.  See the Base Station EEPROM Map for specific memory address details.

##### Command:
Value | # Bytes | Type | Description
------|---------|------|------------
0x73  | 1       | uint8 | Command ID
0xXXXX  | 2       | uint16 | EEPROM address to read
0xXXXX  | 2       | uint16 | Checksum

##### Success Response:
Value | # Bytes | Type | Description
------|---------|------|------------
0x73  | 1       | uint8 | Command ID
0xXXXX  | 2       | uint16 | Value read from EEPROM
0xXXXX  | 2       | uint16 | Checksum
