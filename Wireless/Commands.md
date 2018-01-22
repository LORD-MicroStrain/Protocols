# Wireless Node and Base Station Commands

Note that some commands are device specific.

#### Legacy FW version to ASPP version lookup table

New devices/firmware support `Eeprom 124`, which identifies the ASPP version (msb.lsb) that the device supports for the LXRS communication protocol. `Eeprom 126` identifies the ASPP version for the LXRS+ communication protocol.
The firmware version of the device was originally used to determine the ASPP version. The following lookup table is provided for legacy purposes:

ASPP Version  |  Base Station FW version  |  Node FW version
--------------|---------------------------|-----------------
ASPP v1.5      | -                          |  FW v10.33392
ASPP v1.4      | -                          |  FW v10.31758
ASPP v1.3      | FW v4.30448                |  -
ASPP v1.2      | -                          |  FW v10.0
ASPP v1.1      | FW v4.0                    |  FW v8.21
ASPP v1.0      | FW v1.0                    |  FW v1.0


-----

### Base Station Commands

Command      | Command ID    |  Base Station ASPP Version required
-------------|---------------|--------------------
[Start RF Sweep Mode (v1)](#start-rf-sweep-mode-v1) | 0x00ED | ASPP v1.3
[Start RF Sweep Mode (v1, ASPP3)](#start-rf-sweep-mode-v1-aspp3) | 0x00ED | ASPP v3.0
[Ping Base Station (v1)](#ping-base-station-v1) | 0x01 | ASPP v1.0
[Ping Base Station (v2)](#ping-base-station-v2) | 0x0001 | ASPP v1.1
[Ping Base Station (v2, ASPP3)](#ping-base-station-v2-aspp3) | 0x0001 | ASPP v3.0
[Read Base Station EEPROM (v1)](#read-base-station-eeprom-v1) | 0x73 | ASPP v1.0
[Read Base Station EEPROM (v2)](#read-base-station-eeprom-v2) | 0x0073 | ASPP v1.1
[Read Base Station EEPROM (v2, ASPP3)](#read-base-station-eeprom-v2-aspp3) | 0x0073 | ASPP v3.0
[Write Base Station EEPROM (v1)](#write-base-station-eeprom-v1) | 0x78 | ASPP v1.0
[Write Base Station EEPROM (v2)](#write-base-station-eeprom-v2) | 0x0078 | ASPP v1.1
[Write Base Station EEPROM (v2, ASPP3)](#write-base-station-eeprom-v2-aspp3) | 0x0078 | ASPP v3.0
[Enable Beacon (v1)](#enable-beacon-v1) | 0xBEAC | ASPP v1.0
[Enable Beacon (v2)](#enable-beacon-v2) | 0xBEAC | ASPP v1.1
[Enable Beacon (v2, ASPP3)](#enable-beacon-v2-aspp3) | 0xBEAC | ASPP v3.0
[Disable Beacon (v1)](#disable-beacon-v1) | 0xBEAC | ASPP v1.0
[Disable Beacon (v2)](#disable-beacon-v2) | 0xBEAC | ASPP v1.1
[Disable Beacon (v2, ASPP3)](#disable-beacon-v2-aspp3) | 0xBEAC | ASPP v3.0
[Beacon Status (v1)](#beacon-status-v1) | 0xBEAD | ASPP v1.1
[Beacon Status (v1, ASPP3)](#beacon-status-v1-aspp3) | 0xBEAD | ASPP v3.0
[Update Beacon Time (v1)](#update-beacon-time-v1) | 0xBEAB | ASPP v1.1
[Update Beacon Time (v1, ASPP3)](#update-beacon-time-v1-aspp3) | 0xBEAB | ASPP v3.0
[Cycle Base Station Power & Radio (v1)](#cycle-base-station-power--radio-v1) | - | ASPP v1.0
[Cycle Base Station Power & Radio (v2)](#cycle-base-station-power--radio-v2) | 0x0030 | ASPP v3.0
[(Legacy) Node Quick Ping (v1)*](#legacy-node-quick-ping-v1) | 0x02 | ASPP v1.0
[(Legacy) Node Quick Ping (v2)*](#legacy-node-quick-ping-v2) | 0x0012 | ASPP v1.6
[Set Node to Idle (v1)*](#set-node-to-idle-v1) | 0x0090 | ASPP v1.0
[Set Node to Idle (v2)*](#set-node-to-idle-v2) | 0x0090 | ASPP v1.6
[Set Node to Idle (v2, ASPP3)*](#set-node-to-idle-v2-aspp3) | 0x0090 | ASPP v3.0
[Test Node Communication Protocol(v1)*](#test-node-communication-protocol-v1) | 0x0013 | ASPP v1.7
[Test Node Communication Protocol(v1, ASPP3)*](#test-node-communication-protocol-v1-aspp3) | 0x0013 | ASPP v3.0

*This command targets a Node, but is handled by the Base Station itself.

### Node Commands

Command      | Command ID    |  Node ASPP Version required
-------------|---------------|--------------------
[Ping (v1)](#ping-v1) | 0x0002 | ASPP v1.0
[Ping (v1, ASPP3)](#ping-v1-aspp3) | 0x0002 | ASPP v3.0
[Initiate Sleep Mode (v1)](#initiate-sleep-mode-v1) | 0x32 | ASPP v1.0
[Initiate Sleep Mode (v2)](#initiate-sleep-mode-v2) | 0x0032 | ASPP v1.8
[Initiate Sleep Mode (v2, ASPP3)](#initiate-sleep-mode-v2-aspp3) | 0x0032 | ASPP v3.0
[Read Node EEPROM (v1)](#read-node-eeprom-v1) | 0x0003 | ASPP v1.0
[Read Node EEPROM (v2)](#read-node-eeprom-v2) | 0x0007 | ASPP v1.1
[Read Node EEPROM (v2, ASPP3)](#read-node-eeprom-v2-aspp3) | 0x0007 | ASPP v3.0
[Batch Node EEPROM Read (v1, ASPP3)](#batch-node-eeprom-read-v1-aspp3) | 0x000A | ASPP v3.0
[Write Node EEPROM (v1)](#write-node-eeprom-v1) | 0x0004 | ASPP v1.0
[Write Node EEPROM (v2)](#write-node-eeprom-v2) | 0x0008 | ASPP v1.1
[Write Node EEPROM (v2, ASPP3)](#write-node-eeprom-v2-aspp3) | 0x0008 | ASPP v3.0
[Initiate Synchronized Sampling (v1)](#initiate-synchronized-sampling-v1) | 0x003B | ASPP v1.0
[Initiate Synchronized Sampling (v1, ASPP3)](#initiate-synchronized-sampling-v1-aspp3) | 0x003B | ASPP v3.0
[Initiate Low Duty Cycle (v1)](#initiate-low-duty-cycle-v1) | 0x0038 | ASPP v1.0
[Initiate Low Duty Cycle (v2)](#initiate-low-duty-cycle-v2) | 0x0039 | ASPP v1.5
[Initiate Low Duty Cycle (v2, ASPP3)](#initiate-low-duty-cycle-v2-aspp3) | 0x0039 | ASPP v3.0
[(Legacy) Initiate Real-Time Streaming](#legacy-initiate-real-time-streaming) | 0x38 | ASPP v1.0
[(Legacy) Arm for Datalogging](#legacy-arm-node-for-datalogging) | 0x000D | ASPP v1.0
[(Legacy) Trigger Armed Datalogging](#legacy-trigger-armed-datalogging) | 0x000E | ASPP v1.0
[Get Logged Data (v1)](#get-logged-data-v1) | 0x0041 | ASPP v1.4
[Get Logged Data (v1, ASPP3)](#get-logged-data-v1-aspp3) | 0x0041 | ASPP v3.0
[Page Download](#page-download) | 0x05 | ASPP v1.0
[Log Session Info (v1)](#log-session-info-v1) | 0x0040 | ASPP v1.4
[Log Session Info (v1, ASPP3)](#log-session-info-v1-aspp3) | 0x0040 | ASPP v3.0
[Erase Logged Data (v1)](#erase-logged-data-v1) | 0x06 | ASPP v1.0
[Erase Logged Data (v2)](#erase-logged-data-v2) | 0x0042 | ASPP v1.4
[Erase Logged Data (v2, ASPP3)](#erase-logged-data-v2-aspp3) | 0x0042 | ASPP v3.0
[Auto-Balance Channel (v1)](#auto-balance-channel-v1) | 0x62 | ASPP v1.0
[Auto-Balance Channel (v2)](#auto-balance-channel-v2) | 0x0065 | ASPP v1.2
[Auto-Balance Channel (v2, ASPP3)](#auto-balance-channel-v2-aspp3) | 0x0065 | ASPP v3.0
[Auto-Calibrate (v1)](#auto-calibrate-v1) | 0x0064 | ASPP v1.2
[Auto-Calibrate (v1, ASPP3)](#auto-calibrate-v1-aspp3) | 0x0064 | ASPP v3.0
[Get Diagnostic Info (v1)](#get-diagnostic-info-v1) | 0x0009 | ASPP v1.5
[Get Diagnostic Info (v1, ASPP3)](#get-diagnostic-info-v1-aspp3) | 0x0009 | ASPP v3.0
[Read Single Sensor](#read-single-sensor) | 0x03 | ASPP v1.0
[Cycle Power & Radio (v1)](#cycle-power--radio-v1) | - | ASPP v1.0
[Cycle Power & Radio (v1, ASPP3)](#cycle-power--radio-v1-aspp3) | 0x0031 | ASPP v3.0


-----


### Base Station Received Response
When sending Node Commands, a Base Station that supports ASPP 1.8+ (LXRS), or ASPP 3.0+ (LXRS+), will respond with a `Base Station Received Response` packet that indicates the command was received and sent to the Node. This response packet allows you to adjust your timeout and fail earlier, in the case that a Node is out of range, or in a mode that can't be communicated with (sampling, sleeping).

Base Stations with older protocols may respond with a single `0xAA` byte to indicate the command was received and sent to the Node.

##### ASPP 1.8+ Base Station Received Response
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x34;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x09;                    //Payload Length
uint16_t commandId;                                       //Command ID Echo
uint8_t status;                                           //Status byte
float timeUntilComplete;                                  //Estimated time (in seconds) until the next response is expected (0x7F800000 = indefinite until canceled)
uint16_t nodeAddress;                                     //Node Address
uint8_t reserved;                                         //Reserved Byte
uint8_t reserved;                                         //Reserved Byte
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

##### ASPP 3.0+ Base Station Received Response

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x34;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x000B;                  //Payload Length
uint16_t commandId;                                       //Command ID Echo
uint8_t status;                                           //Status byte
float timeUntilComplete;                                  //Estimated time (in seconds) until the next response is expected (0x7F800000 = indefinite until canceled)
uint32_t nodeAddress;                                     //Node Address
uint8_t reserved;                                         //Reserved Byte
uint8_t reserved;                                         //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```


-----


## Ping Base Station (v1)
``ASPP v1.0``

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
```cpp
uint8_t commandId         = 0x01;        //Command ID
```

##### Success Response:
```cpp
uint8_t commandId         = 0x01;        //Command ID Echo
```

##### Failure Response:
None.

<br>

## Ping Base Station (v2)
``ASPP v1.1``

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x02;        //Payload Length
uint16_t commandId        = 0x0001;      //Command ID
uint16_t checksum;                       //Checksum of [stopFlag - commandId]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x02;        //Payload Length
uint16_t commandId        = 0x0001;      //Command ID Echo
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - commandId]
```

##### Failure Response:
None.

<br>

## Ping Base Station (v2, ASPP3)
``ASPP v3.0``

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0002;      //Payload Length
uint16_t commandId        = 0x0001;      //Command ID
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0002;      //Payload Length
uint16_t commandId        = 0x0001;      //Command ID Echo
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Failure Response:
None.

<br>

## Read Base Station EEPROM (v1)
``ASPP v1.0``

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t commandId         = 0x73;        //Command ID
uint16_t eepromAddress;                  //EEPROM address to read
uint16_t checksum;                       //Checksum of [eepromAddress]
```

##### Success Response:
```cpp
uint8_t commandId         = 0x73;        //Command ID Echo
uint16_t value;                          //Value read from EEPROM
uint16_t checksum;                       //Checksum of [value]
```

##### Fail Response:
```cpp
uint8_t failId            = 0x21;        //Fail ID
```

<br>

## Read Base Station EEPROM (v2)
``ASPP v1.1``

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x04;        //Payload Length
uint16_t commandId        = 0x0073;      //Command ID
uint16_t eepromAddress;                  //EEPROM Address to Read
uint16_t checksum;                       //Checksum of [stopFlag - eepromAddress]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0x0073;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Read
uint16_t value;                          //Value Read from EEPROM
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - value]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x05;        //Payload Length
uint16_t commandId        = 0x0073;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Attempted to Read
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
4            | Hardware Error

<br>

## Read Base Station EEPROM (v2, ASPP3)
``ASPP v3.0``

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0004;      //Payload Length
uint16_t commandId        = 0x0073;      //Command ID
uint16_t eepromAddress;                  //EEPROM Address to Read
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0x0073;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Read
uint16_t value;                          //Value Read from EEPROM
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0005;      //Payload Length
uint16_t commandId        = 0x0073;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Attempted to Read
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```
**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
4            | Hardware Error

<br>

## Write Base Station EEPROM (v1)
``ASPP v1.0``

The **Write Base Station EEPROM** command is used to write a value to a specific memory address on the Base Station's EEPROM.

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t commandId         = 0x78;        //Command ID
uint16_t eepromAddress;                  //EEPROM address to write to
uint16_t value;                          //Value to write to EEPROM
uint16_t checksum;                       //Checksum of [eepromAddress - value]
```

##### Success Response:
```cpp
uint8_t commandId         = 0x78;        //Command ID Echo
uint16_t value;                          //Value written to EEPROM
uint16_t checksum;                       //Checksum of [value]
```

##### Fail Response:
```cpp
uint8_t failId            = 0x21;        //Fail ID
```

<br>

## Write Base Station EEPROM (v2)
``ASPP v1.1``

The **Write Base Station EEPROM** command is used to write a value to a specific memory address on the Base Station's EEPROM.

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0x0078;      //Command ID
uint16_t eepromAddress;                  //EEPROM Address to Write to
uint16_t value;                          //Value to Write to EEPROM
uint16_t checksum;                       //Checksum of [stopFlag - value]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0x0078;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Written to
uint16_t value;                          //Value Written
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - value]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x07;        //Payload Length
uint16_t commandId        = 0x0078;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Attempted to Write
uint16_t value;                          //Value Attempted to Write
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
2            | Value out of Bounds
3            | EEPROM Address is read-only
4            | Hardware Error

<br>


## Write Base Station EEPROM (v2, ASPP3)
``ASPP v3.0``

The **Write Base Station EEPROM** command is used to write a value to a specific memory address on the Base Station's EEPROM.

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0x0078;      //Command ID
uint16_t eepromAddress;                  //EEPROM Address to Write to
uint16_t value;                          //Value to Write to EEPROM
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0x0078;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Written to
uint16_t value;                          //Value Written
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0007;      //Payload Length
uint16_t commandId        = 0x0078;      //Command ID Echo
uint16_t eepromAddress;                  //EEPROM Address Attempted to Write
uint16_t value;                          //Value Attempted to Write
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```
**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
2            | Value out of Bounds
3            | EEPROM Address is read-only
4            | Hardware Error

<br>

## Enable Beacon (v1)
``ASPP v1.0``

The **Enable Beacon** command is used to turn on the beacon on the Base Station.<br>
The beacon is used to synchronize and start a group of nodes when performing Synchronized Sampling.

##### Command:
```cpp
uint16_t commandId         = 0xBEAC;      //Command ID
uint32_t timestamp;                       //Timestamp to give to the Beacon
```

##### Success Response:
```cpp
uint16_t commandId         = 0xBEAC;      //Command ID Echo
```

##### Fail Response:
None.

##### Notes:
**Command Timestamp**: The last 4 bytes in the Command Packet are Timestamp bytes. The beacon that is started from this command will send a Timestamp beginning from this value. These bytes represent the current UTC time in seconds from the Unix Epoch (January 1, 1970).

<br>

## Enable Beacon (v2)
``ASPP v1.1``

The **Enable Beacon** command is used to turn on the beacon on the Base Station.<br>
The beacon is used to synchronize and start a group of nodes when performing Synchronized Sampling.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID
uint32_t timestamp;                      //Timestamp to give to the Beacon
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t timestamp;                      //Timestamp given to the Beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x07;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t timestamp;                      //Timestamp Attempted to Set
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

<br>

## Enable Beacon (v2, ASPP3)
``ASPP v3.0``

The **Enable Beacon** command is used to turn on the beacon on the Base Station.<br>
The beacon is used to synchronize and start a group of nodes when performing Synchronized Sampling.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID
uint32_t timestamp;                      //Timestamp to give to the Beacon
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t timestamp;                      //Timestamp given to the Beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0007;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t timestamp;                      //Timestamp Attempted to Set
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```
**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

<br>

## Disable Beacon (v1)
``ASPP v1.0``

The **Disable Beacon** command is used to turn off the beacon on the Base Station.

##### Command:
```cpp
uint16_t commandId         = 0xBEAC;      //Command ID
uint32_t disableBeacon     = 0xFFFFFFFF;  //Value to disable the beacon
```

##### Success Response:
```cpp
uint16_t commandId         = 0xBEAC;      //Command ID Echo
```
##### Fail Response:
None.

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.

<br>

## Disable Beacon (v2)
``ASPP v1.1``

The **Disable Beacon** command is used to turn off the beacon on the Base Station.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x07;        //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.

<br>

## Disable Beacon (v2, ASPP3)
``ASPP v3.0``

The **Enable Beacon** command is used to turn on the beacon on the Base Station.<br>
The beacon is used to synchronize and start a group of nodes when performing Synchronized Sampling.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0007;      //Payload Length
uint16_t commandId        = 0xBEAC;      //Command ID Echo
uint32_t disableBeacon    = 0xFFFFFFFF;  //Value to Disable the Beacon
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```
**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.

<br>

## Beacon Status (v1)
``ASPP v1.1``

The **Beacon Status** command is used to get information about the Beacon on the Base Station.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x02;        //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID
uint16_t checksum;                       //Checksum of [stopFlag - commandId]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x0B;        //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID Echo
uint8_t beaconStatus;                    //The Status of the Beacon
uint32_t timestamp_sec;                  //The Current Timestamp of the Beacon (seconds)
uint32_t timestamp_nano;                 //The Current Timestamp of the Beacon (nanoseconds)
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - timestamp_nano]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x03;        //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID Echo
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```

**beaconStatus**

 - 0x00 - Beacon is Off
 - 0x01 - Beacon is On

**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

<br>

## Beacon Status (v1, ASPP3)
``ASPP v3.0``

The **Beacon Status** command is used to get information about the Beacon on the Base Station.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0002;      //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x000B;      //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID Echo
uint8_t beaconStatus;                    //The Status of the Beacon
uint32_t timestamp_sec;                  //The Current Timestamp of the Beacon (seconds)
uint32_t timestamp_nano;                 //The Current Timestamp of the Beacon (nanoseconds)
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0003;      //Payload Length
uint16_t commandId        = 0xBEAD;      //Command ID Echo
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

**beaconStatus**

 - 0x00 - Beacon is Off
 - 0x01 - Beacon is On

**Error Codes:**

Code         | Description
-------------|--------------
4            | Hardware Error

<br>

## Update Beacon Time (v1)
``ASPP v1.1``

The **Update Beacon Time** command is used to update the time that is used by the beacon without re-enabling the beacon. This can be useful when relying on a PPS for time synchronization and not the internal clock. In most scenarios, the **Enable Beacon** command should be used to set the beacon time while enabling the beacon.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID
uint32_t timestamp;                      //Timestamp to give to the Beacon
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x06;        //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID Echo
uint32_t timestamp;                      //Timestamp given to the beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x07;        //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID Echo
uint32_t timestamp;                      //Timestamp attempted to set
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - errorCode]
```

<br>

## Update Beacon Time (v1, ASPP3)
``ASPP v3.0``

The **Update Beacon Time** command is used to update the time that is used by the beacon without re-enabling the beacon. This can be useful when relying on a PPS for time synchronization and not the internal clock. In most scenarios, the **Enable Beacon** command should be used to set the beacon time while enabling the beacon.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID
uint32_t timestamp;                      //Timestamp to give to the Beacon
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0006;      //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID Echo
uint32_t timestamp;                      //Timestamp given to the beacon
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Fail Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x32;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x0007;      //Payload Length
uint16_t commandId        = 0xBEAB;      //Command ID Echo
uint32_t timestamp;                      //Timestamp attempted to set
uint8_t errorCode;                       //Error Code
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

<br>

## Cycle Base Station Power & Radio (v1)
``ASPP v1.0``

To cycle the power on the BaseStation, use the `Write EEPROM` command and write a `1` to `EEPROM 250`.

To cycle the radio on the BaseStation, use the `Write EEPROM` command and write a `2` to `EEPROM 250`.

<br>

## Cycle Base Station Power & Radio (v2)
``ASPP v3.0``

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x01;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0030;                  //Command ID
uint8_t resetType;                                        //Reset Type (1 = hard reset, 2 = soft reset)
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0030;                  //Command ID Echo
uint8_t resetType;                                        //Reset Type Echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
none

<br>

## Start RF Sweep Mode (v1)
``ASPP v1.3``

The **Start RF Sweep Mode** command puts the Base Station into a mode where radio frequencies can be scanned for traffic.
All other over-the-air data will be ignored when this mode is active.
To cancel this mode, send any byte or command to the Base Station.

##### Command:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x0E;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x0E;        //Payload Length
uint16_t commandId        = 0x00ED;      //Command ID
uint16_t options;                        //Options (Used internally)
uint32_t minFreq;                        //Minimum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t maxFreq;                        //Maximum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t interval;                       //The Sweep interval in kHz.
uint16_t checksum;                       //Checksum of [stopFlag - interval]
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAA;        //Start of Packet byte
uint8_t stopFlag          = 0x07;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint16_t baseAddress      = 0x1234;      //Base Station Address
uint8_t payloadLen        = 0x0E;        //Payload Length
uint16_t commandId        = 0x00ED;      //Command ID Echo
uint16_t optionsEcho;                    //Options Echo
uint32_t minFreqEcho;                    //Minimum Sweep Frequency Echo
uint32_t maxFreqEcho;                    //Maximum Sweep Frequency Echo
uint32_t intervalEcho;                   //The Sweep interval Echo
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint16_t checksum;                       //Checksum of [stopFlag - intervalEcho]
```

##### Notes:

If the device cannot support the requested parameters, they will be clamped to the closest valid value.
The data packets will relect such changes.

<br>

## Start RF Sweep Mode (v1, ASPP3)
``ASPP v3.0``

The **Start RF Sweep Mode** command puts the Base Station into a mode where radio frequencies can be scanned for traffic.
All other over-the-air data will be ignored when this mode is active.
To cancel this mode, send any byte or command to the Base Station.

##### Command:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x01;        //Delivery Stop Flag
uint8_t appDataType       = 0x30;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x000E;      //Payload Length
uint16_t commandId        = 0x00ED;      //Command ID
uint16_t options;                        //Options (Used internally)
uint32_t minFreq;                        //Minimum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t maxFreq;                        //Maximum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t interval;                       //The Sweep interval in kHz.
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint8_t RESERVED          = 0x7F;        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Success Response:
```cpp
uint8_t startByte         = 0xAC;        //Start of Packet byte
uint8_t stopFlag          = 0x08;        //Delivery Stop Flag
uint8_t appDataType       = 0x31;        //App Data Type
uint32_t baseAddress      = 0x00001234;  //Base Station Address
uint16_t payloadLen       = 0x000E;      //Payload Length
uint16_t commandId        = 0x00ED;      //Command ID Echo
uint16_t optionsEcho;                    //Options Echo
uint32_t minFreqEcho;                    //Minimum Sweep Frequency Echo
uint32_t maxFreqEcho;                    //Maximum Sweep Frequency Echo
uint32_t intervalEcho;                   //The Sweep interval Echo
uint8_t RESERVED;                        //Reserved Byte
uint8_t RESERVED;                        //Reserved Byte
uint32_t checksum;                       //CRC Checksum of all bytes
```

##### Notes:

If the device cannot support the requested parameters, they will be clamped to the closest valid value.
The data packets will relect such changes.

<br>

## (Legacy) Node Quick Ping (v1)
``ASPP v1.0``

``Legacy Command - This command is no longer supported by our latest products``

The **Quick Ping** command is used to check the communication between the Base Station and the Node. This command has a direct success/fail response, so it can immediately tell you whether communication was successful. Other commands,do not have a fail response, requiring you to use a timeout to determine a failure.

##### Command:
```cpp
uint8_t commandId              = 0x02;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
```

##### Success Response:
```cpp
uint8_t commandId              = 0x02;                    //Command ID Echo
```

##### Failure Response:
```cpp
uint8_t failId                 = 0x21;                    //Failure ID
```

<br>

## (Legacy) Node Quick Ping (v2)
``ASPP v1.6``

``Legacy Command - This command is no longer supported by our latest products``

The **Quick Ping** command is used to check the communication between the Base Station and the Node. This command has a direct success/fail response, so it can immediately tell you whether communication was successful. Other commands,do not have a fail response, requiring you to use a timeout to determine a failure.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x0E;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0012;                  //Command ID
uint16_t nodeAddress;                                     //Node Address
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint16_t baseAddress;                                     //Base Station Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0012;                  //Command ID Echo
uint16_t nodeAddress;                                     //Node Address
int8_t reserved;                                          //Reserved Byte
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

##### Failure Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x32;                    //App Data Type
uint16_t baseAddress;                                     //Base Station Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0012;                  //Command ID Echo
uint16_t nodeAddress;                                     //Node Address
int8_t reserved1;                                         //Reserved Byte
int8_t reserved2;                                         //Reserved Byte
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

<br>

## Set Node to Idle (v1)
``ASPP v1.0``

The **Set to Idle** command is used to put a Node that is sampling, or sleeping, back into the Idle Mode so that it may be communicated with.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0xFE;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0090;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
The Node was set to idle and can now be communicated with.
```cpp
uint8_t commandId              = 0x90;                    //Command ID Echo
uint8_t commandCeased          = 0x01;                    //The Set to Idle command has ceased
```

##### Failure Response:
The Set to Idle process was aborted.
```cpp
uint8_t failId                 = 0x21;                    //Failed/Aborted ID
uint8_t commandCeased          = 0x01;                    //The Set to Idle command has ceased
```

##### Notes:
**Ongoing Operation:** The Set to Idle command puts the Base Station in a mode that sends small packets as fast as possible in an attempt to communicate with the Node. The Base Station will periodically check to see if the Node has responded to a ping request. The function will continue indefinitely until either the Node responds, or the user sends any byte to the Base Station, which cancels the operation. No incoming packets will be heard while the Base Station is in this mode.

**Broadcast Special Case:** When the broadcast Node address 65535 (0xFFFF) is used, the Base Station does not check for a ping response. It will continue sending the Set to Idle command until interrupted by the user (any single byte sent to the Base Station). This will attempt to set all Nodes to idle on the current frequency that the Base Station is on.

<br>

## Set Node to Idle (v2)
``ASPP v1.6``

The **Set to Idle** command is used to put a Node that is sampling, or sleeping, back into the Idle Mode so that it may be communicated with.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x0E;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0091;                  //Command ID
uint16_t nodeAddress;                                     //Node Address
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Completion Response:
The set to idle operation has completed. Check the completion status flag for success or canceled.

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint16_t baseAddress;                                     //Base Station Address
uint8_t payloadLen             = 0x05;                    //Payload Length
uint16_t commandId             = 0x0091;                  //Command ID Echo
uint16_t nodeAddress;                                     //Node Address
uint8_t statusFlag;                                       //Completion Status Flag (0 = success, 1 = canceled)
int8_t reserved;                                          //Reserved Byte
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - statusFlag]
```

##### Notes:
**Ongoing Operation:** The Set to Idle command puts the Base Station in a mode that sends small packets as fast as possible in an attempt to communicate with the Node. The Base Station will periodically check to see if the Node has responded to a ping request. The function will continue indefinitely until either the Node responds, or the user sends any byte to the Base Station, which cancels the operation. No incoming packets will be heard while the Base Station is in this mode.

**Broadcast Special Case:** When the broadcast Node address 65535 (0xFFFF) is used, the Base Station does not check for a ping response. It will continue sending the Set to Idle command until interrupted by the user (any single byte sent to the Base Station). This will attempt to set all Nodes to idle on the current frequency that the Base Station is on.

<br>

## Set Node to Idle (v2, ASPP3)
``ASPP v3.0``

The **Set to Idle** command is used to put a Node that is sampling, or sleeping, back into the Idle Mode so that it may be communicated with.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x01;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0006;                  //Payload Length
uint16_t commandId             = 0x0091;                  //Command ID
uint32_t nodeAddress;                                     //Node Address
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Completion Response:
The set to idle operation has completed. Check the completion status flag for success or canceled.

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0007;                  //Payload Length
uint16_t commandId             = 0x0091;                  //Command ID Echo
uint32_t nodeAddress;                                     //Node Address
uint8_t statusFlag;                                       //Completion Status Flag (0 = success, 1 = canceled)
uint8_t reserved;                                         //Reserved Byte
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Notes:
**Ongoing Operation:** The Set to Idle command puts the Base Station in a mode that sends small packets as fast as possible in an attempt to communicate with the Node. The Base Station will periodically check to see if the Node has responded to a ping request. The function will continue indefinitely until either the Node responds, or the user sends any byte to the Base Station, which cancels the operation. No incoming packets will be heard while the Base Station is in this mode.

**Broadcast Special Case:** When the broadcast Node address 4294967295(0xFFFFFFFF) is used, the Base Station does not check for a ping response. It will continue sending the Set to Idle command until interrupted by the user (any single byte sent to the Base Station). This will attempt to set all Nodes to idle on the current frequency that the Base Station is on.

<br>

## Test Node Communication Protocol (v1)
``ASPP v1.7``

The **Test Node Communication Protocol** command is used to test changing the communication protocol of a Node. This is useful, as it is possible to switch a Node from LXRS mode to LXRS+ mode, and then no longer be able to communicate with it due to the reduced range. The BaseStation will switch the Node to the specified protocol, switch itself over to the specified protocol, and attempt to ping the Node. After the command completes, the BaseStation and Node will be changed back to the original communication protocol.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x0E;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID
uint16_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode (0 - LXRS, 1 - LXRS+)
uint16_t checksum;                                        //Checksum of [stopFlag - mode]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
This response indicates the Node successfully responded to pings on the new communication protocol.

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID Echo
uint16_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode Echo
int8_t reserved;                                          //Reserved Byte
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

##### Failure Response:
This response indicates the Node failed to respond to pings on the new communication protocol.

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x32;                    //App Data Type
uint16_t baseAddress           = 0x1234;                  //Base Station Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID Echo
uint16_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode Echo
uint8_t errorCode;                                        //Error Code
int8_t reserved1;                                         //Reserved Byte
int8_t reserved2;                                         //Reserved Byte
uint16_t checksum;                                        //Checksum of [stopFlag - nodeAddress]
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Invalid Mode Specified
2            | Invalid duration specified by BaseStation (< 0 or > 5)
3            | No response received after sending switch mode node command
4            | Failed to ping Node after switching modes

<br>

## Test Node Communication Protocol (v1, ASPP3)
``ASPP v3.0``

The **Test Node Communication Protocol** command is used to test changing the communication protocol of a Node. This is useful, as it is possible to switch a Node from LXRS mode to LXRS+ mode, and then no longer be able to communicate with it due to the reduced range. The BaseStation will switch the Node to the specified protocol, switch itself over to the specified protocol, and attempt to ping the Node. After the command completes, the BaseStation and Node will be changed back to the original communication protocol.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x01;                    //Delivery Stop Flag
uint8_t appDataType            = 0x30;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0008;                  //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID
uint32_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode (0 - LXRS, 1 - LXRS+)
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
This response indicates the Node successfully responded to pings on the new communication protocol.

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x31;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0008;                  //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID Echo
uint32_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode Echo
uint8_t reserved;                                         //Reserved Byte
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
This response indicates the Node failed to respond to pings on the new communication protocol.

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x32;                    //App Data Type
uint32_t baseAddress           = 0x00001234;              //Base Station Address
uint16_t payloadLen            = 0x0009;                  //Payload Length
uint16_t commandId             = 0x0013;                  //Command ID Echo
uint32_t nodeAddress;                                     //Node Address
uint16_t mode;                                            //Protocol mode Echo
uint8_t errorCode;                                        //Error Code
uint8_t reserved1;                                        //Reserved Byte
uint8_t reserved2;                                        //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Invalid Mode Specified
2            | Invalid duration specified by BaseStation (< 0 or > 5)
3            | No response received after sending switch mode node command
4            | Failed to ping Node after switching modes

-------

## Ping (v1)
``ASPP v1.0``

The **Ping** command is used to check the communication between the Base Station and the Node, and gives more information (like node RSSI) than the Quick Ping command. This is useful for range tests.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0002;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t notUsed               = 0x0000;                  //Empty Payload (not used)
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - notUsed]
```

##### Failure Response:
No Response.

<br>

## Ping (v1, ASPP3)
``ASPP v3.0``

The **Ping** command is used to check the communication between the Base Station and the Node.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0002;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0002;                  //Command ID echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
No Response.

<br>

## Initiate Sleep Mode (v1)
``ASPP v1.0``

The **Initiate Sleep Mode** command is used to put the Node in a low power state. When the Node is in this low power Sleep Mode, it will not hear any commands except for the Set to Idle command, which will wake the node and put it back into its normal, idle state. The Node should be put into Sleep Mode when you no longer needs to communicate with the node, but want to keep it powered on and preserve battery life.

##### Command:
```cpp
uint8_t commandId              = 0x32;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
```

##### Success Response:
No Response.

##### Failure Response:
No Response.

##### Notes:
**Waking a Node:** A Node in Sleep Mode periodically awakes, listens for a Set to Idle command, and if none is received, returns to sleep. To wake a sleeping Node, send the Set to Idle command.

**Sleep Interval:** The Node’s Sleep Interval is the interval at which the Node will awake and listen for the Set to Idle command. See the Node EEPROM map for more details.

**User Inactivity Timeout:** The Node's User Inactivity Timeout is the length of time, without user activity, before the Node enters its Default Mode. If the Default Mode is idle, or sleep, the Node will automatically enter Sleep Mode when this timeout expires. See the Node EEPROM map for more details.

<br>

## Initiate Sleep Mode (v2)
``ASPP v1.8``

The **Initiate Sleep Mode** command is used to put the Node in a low power state. When the Node is in this low power Sleep Mode, it will not hear any commands except for the Set to Idle command, which will wake the node and put it back into its normal, idle state. The Node should be put into Sleep Mode when you no longer needs to communicate with the node, but want to keep it powered on and preserve battery life.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0032;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0032;                  //Command ID Echo
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Failure Response:
No Response.

<br>

## Initiate Sleep Mode (v2, ASPP3)
``ASPP v3.0``

The **Initiate Sleep Mode** command is used to put the Node in a low power state. When the Node is in this low power Sleep Mode, it will not hear any commands except for the Set to Idle command, which will wake the node and put it back into its normal, idle state. The Node should be put into Sleep Mode when you no longer needs to communicate with the node, but want to keep it powered on and preserve battery life.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0032;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0032;                  //Command ID echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
No Response.

<br>

## Read Node EEPROM (v1)
``ASPP v1.0``

The **Read Node EEPROM** command is used to read the value of a specific memory address from the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0003;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Read
uint16_t checksum;                                        //Checksum of [stopFlag - eepromAddress]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x00;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t eepromVal;                                       //Value Read from EEPROM
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - eepromVal]
```

##### Failure Response:
No Response.

<br>

## Read Node EEPROM (v2)
``ASPP v1.1``

The **Read Node EEPROM** command is used to read the value of a specific memory address from the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x04;                    //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Read
uint16_t checksum;                                        //Checksum of [stopFlag - eepromAddress]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Read
uint16_t eepromVal;                                       //Value Read from EEPROM
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - eepromVal]
```

##### Failure Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x05;                    //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Echo
uint8_t errorCode;                                        //Error Code
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - errorCode]
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
4            | Hardware Error

<br>

## Read Node EEPROM (v2, ASPP3)
``ASPP v3.0``

The **Read Node EEPROM** command is used to read the value of a specific memory address from the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0004;                  //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Read
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0006;                  //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Read
uint16_t eepromValue;                                     //Value Read from EEPROM
uint8_t notUsed;                                          //RESERVED
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x05;                    //Payload Length
uint16_t commandId             = 0x0007;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Echo
uint8_t errorCode;                                        //Error Code
uint8_t notUsed;                                          //RESERVED
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
4            | Hardware Error

<br>

## Batch Node EEPROM Read (v1, ASPP3)
``ASPP v3.0``

The **Batch Node EEPROM Read** command is used to read a group of ordered EEPROM locations from the Node, starting with the address specified in the command. The Node will response will ordered eeprom address and value pairs from the specified address until the packet is full or the Node has no larger addressed eeproms. Eeproms that are not supported by the Node will not be sent in the response.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0004;                  //Payload Length
uint16_t commandId             = 0x000A;                  //Command ID
uint16_t startAddress;                                    //EEPROM Address to start reading at
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen;                                      //Payload Length
uint16_t commandId             = 0x000A;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address read
uint16_t eepromValue;                                     //EEPROM value for the given address
//repeat eepromAddress and eepromValue until packet is filled or there are no higher eeprom addresses
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

<br>

## Write Node EEPROM (v1)
``ASPP v1.0``

The **Write Node EEPROM** command is used to write a value to a specific memory address on the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0004;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Write to
uint16_t value;                                           //Value to Write to EEPROM
uint16_t checksum;                                        //Checksum of [stopFlag - value]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x00;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0004;                  //Command ID Echo
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Failure Response:
No Response.

<br>

## Write Node EEPROM (v2)
``ASPP v1.1``

The **Write Node EEPROM** command is used to write a value to a specific memory address on the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Write to
uint16_t value;                                           //Value to Write to EEPROM
uint16_t checksum;                                        //Checksum of [stopFlag - value]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Written to
uint16_t valueWritten;                                    //Value Written to EEPROM
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - valueWritten]
```

##### Failure Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Echo
uint16_t valueWritten;                                    //Value Written Echo
uint8_t errorCode;                                        //Error Code
int8_t notUsed;                                           //RESERVED
int8_t baseRssi;                                          //Base RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - errorCode]
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
2            | Value out of Bounds
3            | EEPROM Address is read-only
4            | Hardware Error

<br>

## Write Node EEPROM (v2, ASPP3)
``ASPP v3.0``

The **Write Node EEPROM** command is used to write a value to a specific memory address on the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0006;                  //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID
uint16_t eepromAddress;                                   //EEPROM Address to Write to
uint16_t value;                                           //Value to Write to EEPROM
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0006;                  //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Written to
uint16_t valueWritten;                                    //Value Written to EEPROM
uint8_t notUsed;                                          //RESERVED
uint8_t baseRssi;                                         //Base RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0007;                  //Payload Length
uint16_t commandId             = 0x0008;                  //Command ID Echo
uint16_t eepromAddress;                                   //EEPROM Address Echo
uint16_t valueWritten;                                    //Value Written Echo
uint8_t errorCode;                                        //Error Code
uint8_t notUsed;                                          //RESERVED
uint8_t baseRssi;                                         //Base RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

**Error Codes:**

Code         | Description
-------------|--------------
1            | Unknown EEPROM Address
2            | Value out of Bounds
3            | EEPROM Address is read-only
4            | Hardware Error

<br>

## (Legacy) Arm Node for Datalogging
``ASPP v1.0``

``Legacy Command - This command is no longer supported by our latest products``

Use the **Arm Node** command to put the node in an armed state waiting for the [Trigger Armed Datalogging](#trigger-armed-datalogging) command.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02 + # of user bytes;  //Payload Length
uint16_t commandId             = 0x000D;                  //Command ID
int8_t userBytes[0-50];                                   //up to 50 (optional) user entered bytes
uint16_t checksum;                                        //Checksum of [stopFlag - userBytes]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x03;                    //Payload Length
uint16_t commandId             = 0x000D;                  //Command ID Echo
uint8_t reserved1;                                        //RESERVED
int8_t reserved2;                                         //RESERVED
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - reserved1]
```

##### Failure Response:
No Response.

##### Notes:
**User Entered Bytes:** You may send up to 50 bytes with the Arm Command which will then be in the header information of the packet when the data is downloaded from the node using the [Page Download](#page-download) command.

**Disarming:** A Node will stay in this armed state for a default of 10 seconds (EEPROM adjustable). To disarm an Armed Node manually, use the [Set to Idle](#set-to-idle) command.

<br>

## (Legacy) Trigger Armed Datalogging
``ASPP v1.0``

``Legacy Command - This command is no longer supported by our latest products``

The **Trigger Armed Datalogging** command is used to initiate a data capture session on-board the Node.The data will be stored in the Node's internal memory and may be downloaded at a later time.

In most cases, you will want to [Arm](#arm-node-for-datalogging) each Node individually, and then send this command to the broadcast Node Address (65535 or 0xFFFF). This will be sent to all nodes on the Base Station's operating frequency, and any Nodes that are in the "Armed" state will start datalogging. This can be useful to start datalogging on multiple nodes at the same time.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x0A;                    //Payload Length
uint16_t commandId             = 0x000E;                  //Command ID
uint32_t timestampSec;                                    //UTC Timestamp (Seconds)
uint32_t timestampNano;                                   //UTC Timestamp (Nanoseconds)
uint16_t checksum;                                        //Checksum of [stopFlag - timestampNano]
```

##### Success Response:
No Response.

##### Failure Response:
No Response.

##### Notes:
**Timestamp:** The Timestamp is made up of 2 values, each of which are 4 bytes. The first value represents the seconds of the timestamp, and the second value represents the nanoseconds of the timestamp. When downloading the logged data from the node, this timestamp will be transmitted in the header information and can be used to determine the exact timestamp of each data point. These bytes represent the current UTC time in seconds from the Unix Epoch (January 1, 1970).

<br>

## Page Download
``ASPP v1.0``

The **Page Download** command is used to retrieve a logged data session from the Node. Note that it can also be used to read large chunks of EEPROM values as well.

##### Command:
```cpp
uint8_t commandId              = 0x05;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
uint16_t pageIndex;                                       //Index of Page to download
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t commandId              = 0x05;                    //Command ID Echo
uint8_t data[264];                                        //The Page Data (132 2-byte values)
uint16_t checksum;                                        //Checksum of [data]
```

##### Failure Response:
```cpp
uint8_t commandId              = 0x05;                    //Command ID Echo
uint16_t failId                = 0x21;                    //Fail Indicator
```

##### Notes:
**Page Index:** Each Node contains 2MB of memory. These 2MB are mapped to 8192 pages of data, with each page containing 264 bytes.

Pages are numbered sequentially from 0 to 8191:

* **Page 0** contains data points that represent the value in the Node's EEPROM from locations 0 - 254.
* **Page 1** contains data points that represent the value in the Node's EEPROM from locations 256 - 510.
* **Page 2** is the first page that will contain sampled data that was logged to the node.

**Data Sessions:** A Node can contain multiple consecutive datalogging sessions. Each of these sessions has a leading multi-byte header which is used to identify the start of a new datalogging session and the end of the previous session. The header contains the datalogging information stored during that particular session.

**Session Header:** The datalogging session header is a multiple-byte leading string indicating the start of the next session. The header can be found anywhere on a downloaded page and it can wrap between pages. The header can be in one of the following versioned formats:

##### Header Format Version **1.0**:
```cpp
uint16_t startOfHeader         = 0xFFFF;                  //Start of Header
uint8_t headerId               = 0xFD;                    //Header ID
uint8_t triggerId;                                        //Trigger ID
uint8_t headerVerMajor         = 0x01;                    //Header Version (Major)
uint8_t headerVerMinor         = 0x00;                    //Header Version (Minor)
uint16_t numBytesBeforeChInfo;                            //# of Bytes before the Channel Info
uint16_t samplesPerDataSet;                               //Samples per Data Set
uint16_t sessionIndex;                                    //Session Index
uint16_t channelMask;                                     //Active Channel Mask
uint16_t sampleRate;                                      //Sample Rate
uint16_t numUserBytes;                                    //# of User Entered Bytes
int8_t userBytes[0-50];                                   //up to 50 user entered bytes (if any)
uint16_t numBytesPerCh         = 0x000A;                  //# of Bytes per Channel
uint8_t chEquation;                                       //Channel Info: Equation ID (per channel)
uint8_t chUnit;                                           //Channel Info: Unit ID (per channel)
float chSlope;                                            //Channel Info: Slope (per channel)
float chOffset;                                           //Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd     = 0x0008;                  //# of Bytes before end of header
uint32_t timestampSec;                                    //UTC Timestamp (Seconds)
uint32_t timestampNano;                                   //UTC Timestamp (Nanoseconds)
```

##### Header Format Version **2.0**:
```cpp
uint16_t startOfHeader         = 0xFFFF;                  //Start of Header
uint8_t headerId               = 0xFD;                    //Header ID
uint8_t triggerId;                                        //Trigger ID
uint8_t headerVerMajor         = 0x02;                    //NEW: Header Version (Major)
uint8_t headerVerMinor         = 0x00;                    //NEW: Header Version (Minor)
uint16_t numBytesBeforeChInfo;                            //# of Bytes before the Channel Info
uint16_t samplesPerDataSet;                               //Samples per Data Set
uint16_t sessionIndex;                                    //Session Index
uint16_t channelMask;                                     //Active Channel Mask
uint16_t sampleRate;                                      //Sample Rate
uint8_t dataType;                                         //NEW: Data Type
uint8_t reserved;                                         //NEW: RESERVED
uint16_t numUserBytes;                                    //# of User Entered Bytes
int8_t userBytes[0-50];                                   //up to 50 user entered bytes (if any)
uint16_t numBytesPerCh         = 0x000A;                  //# of Bytes per Channel
uint8_t chEquation;                                       //Channel Info: Equation ID (per channel)
uint8_t chUnit;                                           //Channel Info: Unit ID (per channel)
float chSlope;                                            //Channel Info: Slope (per channel)
float chOffset;                                           //Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd     = 0x0008;                  //# of Bytes before end of header
uint32_t timestampSec;                                    //UTC Timestamp (Seconds)
uint32_t timestampNano;                                   //UTC Timestamp (Nanoseconds)
```

##### Header Format Version **2.1**:
```cpp
uint16_t startOfHeader         = 0xFFFF;                  //Start of Header
uint8_t headerId               = 0xFD;                    //Header ID
uint8_t triggerId;                                        //Trigger ID
uint8_t headerVerMajor         = 0x02;                    //NEW: Header Version (Major)
uint8_t headerVerMinor         = 0x01;                    //NEW: Header Version (Minor)
uint16_t numBytesBeforeChInfo;                            //# of Bytes before the Channel Info
uint16_t samplesPerDataSet;                               //NEW: Samples per Data Set / 100
uint16_t sessionIndex;                                    //Session Index
uint16_t channelMask;                                     //Active Channel Mask
uint16_t sampleRate;                                      //Sample Rate
uint8_t dataType;                                         //Data Type
uint8_t reserved;                                         //RESERVED
uint16_t numUserBytes;                                    //# of User Entered Bytes
int8_t userBytes[0-50];                                   //up to 50 user entered bytes (if any)
uint16_t numBytesPerCh         = 0x000A;                  //# of Bytes per Channel
uint8_t chEquation;                                       //Channel Info: Equation ID (per channel)
uint8_t chUnit;                                           //Channel Info: Unit ID (per channel)
float chSlope;                                            //Channel Info: Slope (per channel)
float chOffset;                                           //Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd     = 0x0008;                  //# of Bytes before end of header
uint32_t timestampSec;                                    //UTC Timestamp (Seconds)
uint32_t timestampNano;                                   //UTC Timestamp (Nanoseconds)
```

**Fixed Header:** Each new session is always marked with a 0xFFFF (65535) at its start.

**Header Version:** The header format that needs to be used can be determined by checking the header version bytes.

**Trigger ID:** Each datalogging session has a Trigger ID signifying how the session was started:

Trigger ID   | Description
-------------|--------------
0            | Started via a datalogging command
1            | Ceiling Sensor Event Driven Trigger
2            | Floor Sensor Event Driven Trigger
3            | Ramp Up Sensor Event Driven Trigger
4            | Ramp Down Sensor Event Driven Trigger

**Samples per Data Set:** The number of expected samples per data set. If the session was logged as a continuous datalogging session, this value is not applicable. If the session ended prematurely due to power failure or because
the memory was completely filled, the value will not correspond to the actual number of samples. When parsing session data, the Samples per Data Set value should not be used to determine the end of the session. The end of the session should be determined by the start of the next session header. Header Versions 2.1 and above have the number of Samples per Data Set byte divided by 100 to allow for longer sessions. This value should be multiplied by 100 to obtain the true number of samples.

**Session Index:** Each datalogging session is stored with a session index. The first session’s index is 1 and subsequent sessions would have consecutive index numbers. When the logged sessions are erased the index will be reset, and the first data logging session after the erase will have a Session Index of 1.

**Active Channel Mask:** The channel mask indicates the active channels that were logged in this session.

**Sample Rate:** The Sample Rate that was used during the datalogging session.

**Data Type:** The Data type of which the Node saved data to memory as. The following table shows the possible data values and their corresponding data types:

Value   | Type | Description
--------|------|--------------
1, 3    |uint16_t | A/D value (bits), no conversions (slope & offset) applied
2     |float    | floating point value with any conversions (slope & offset) applied

**User Entered Bytes:** Up to 50 optional user entered bytes may have been sent to the node when triggering an Armed Datalogging session. The *numUserBytes* byte specifies how many user bytes follow in the packet. If the number of user entered bytes is an odd number, there will be 1 extra “buffer” byte appended
to the user data that should be discarded.

**Channel Information:** The Channel Information bytes show which calibration coefficients were enabled during datalogging for each of the active channels.

**Timestamp:** The UTC timestamp represents the starting time of the logged session (the time applied to the very first data point). The nanoseconds should be appended to the seconds of the given timestamp. By incrementing the initial UTC timestamp by the sample rate, you can determine the exact time of each stored data point.

**Session Data:** During the actual datalogging session, the data from each active channel on the Node is written consecutively to the memory pages. For example, a Node with 3 active channels (CH1, CH3, CH4) would write data as CH1, CH3, CH4; CH1, CH3, CH4 and so forth. This data comes off the Node in the same
pattern during download. These byte immediately follow the header bytes.

<br>

## Erase Logged Data (v1)
``ASPP v1.0``

The **Erase Logged Data** command is used to erase all sampled data stored on the Node's memory. This cannot be undone.

##### Command:
```cpp
uint8_t commandId              = 0x06;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
uint32_t commandBytes          = 0x08100CFF;              //Command Bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t commandId              = 0x06;                    //Command ID Echo
```

##### Failure Response:
```cpp
uint8_t failId                 = 0x21;                    //Fail Indicator
```

##### Notes:
**Response:** The response is returned immediately when the erasing processes begins, and no acknowledgment is sent when the process completes. The process may take up to 5 seconds, and the Node will not respond to any commands until the erasing is complete. Completion of the erase can be detected by repeatedly pinging the Node; when the erase is complete, the Node will return to idle mode and respond successfully to the ping.

<br>

## (Legacy) Initiate Real-Time Streaming
``ASPP v1.0``

``Legacy Command - This command is no longer supported by our latest products``

The **Initiate Real-Time Streaming** command is used to start a real-time streaming session on a Node. The Node will respond by immediately sending a stream of data packets as the sensors are read.

**Note:** The Real-Time Streaming sampling mode is a legacy sampling mode and is no longer a recommended method of sampling. The sample rate is not consistent, data is not timestamped, you can only sample 1 Node at a time, and the data packet provides very little information.

##### Command:
```cpp
uint8_t commandId              = 0x38;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
```

##### Response:
Parsing of the streaming packets should begin with the first 0xFF byte. The 0xFF byte is the header of the first valid data packet shown below as Byte 1. Each successive 0xFF indicates the start of a new data packet and the end of the previous packet.

Response Data Packet:
```cpp
uint8_t commandId              = 0xFF;                    //Command ID Echo
uint16_t channelValue;                                    //Channel Value for 1st active channel
//Repeat channelValue bytes for each active channel
uint8_t checksum;                                         //Checksum for [channelValue] bytes
```

##### Notes:
**Terminating Streaming:** Streaming may be stopped at any time by issuing any byte to the Base Station. This will cause the Base Station to stop streaming. It will not however cause the Node to stop streaming. The Node will continue to stream until the set (finite) duration has elapsed, the power on the Node is cycled,
or the Set to Idle command has been issued to the Node.

**End of Stream:** The normal end of a finite stream is marked by 4-6 consecutive 0xAA (170) bytes. When parsing the stream, these bytes should be used as a signal that finite streaming has ended.

<br>

## Initiate Low Duty Cycle (v1)
``ASPP v1.0``

The **Initiate Low Duty Cycle (LDC) v1** command is used to put the Node in LDC (Non-Sync) sampling mode.

The Low Duty Cycle sampling mode is a non-synchronized, low-latency form of sampling. While multiple Nodes can be started sampling, they are not part of a synchronized network. This can cause data packets to be sent over the air at the same time, resulting in data loss. If low-latency is not a requirement, it is highly recommended that you use the Synchronized Sampling Mode.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0038;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
No Response.

##### Failure Response:
No Response.

<br>

## Initiate Low Duty Cycle (v2)
``ASPP v1.5``

The **Initiate Low Duty Cycle (LDC) v2** command is used to put the Node in LDC (Non-Sync) sampling mode. Version 2 of this command adds a timestamp in the command packet, which allows logged data to include a timestamp for use when downloading the data after collection.

The Low Duty Cycle sampling mode is a non-synchronized, low-latency form of sampling. While multiple Nodes can be started sampling, they are not part of a synchronized network. This can cause data packets to be sent over the air at the same time, resulting in data loss. If low-latency is not a requirement, it is highly recommended that you use the Synchronized Sampling Mode.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x0A;                    //Payload Length
uint16_t commandId             = 0x0039;                  //Command ID
uint64_t timestamp;                                       //Current Timestamp (nanoseconds since Unix Epoch)
uint16_t checksum;                                        //Checksum of [stopFlag - timestamp]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0039;                  //Command ID Echo
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Failure Response:
No Response.

<br>

## Initiate Low Duty Cycle (v2, ASPP3)
``ASPP v3.0``

The **Initiate Low Duty Cycle (LDC)** command is used to put the Node in LDC (Non-Sync) sampling mode.

The Low Duty Cycle sampling mode is a non-synchronized, low-latency form of sampling. While multiple Nodes can be started sampling, they are not part of a synchronized network. This can cause data packets to be sent over the air at the same time, resulting in data loss. If low-latency is not a requirement, it is highly recommended that you use the Synchronized Sampling Mode.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x000A;                  //Payload Length
uint16_t commandId             = 0x0039;                  //Command ID
uint64_t timestamp;                                       //Current Timestamp (nanoseconds since Unix Epoch)
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0039;                  //Command ID Echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
No Response.

<br>

## Initiate Synchronized Sampling (v1)
``ASPP v1.0``

The **Initiate Synchronized Sampling command** is used to put the Node into Synchronized Sampling mode. Once in this mode, the node must receive a beacon from the Base Station to begin sampling and transmitting data packets.

For Synchronized Sampling mode, the wireless sensor network needs to be configured so that each node is assigned an appropriate TDMA slot prior to issuing the Initiate Synchronized Sampling command. To set up the wireless sensor network, use either the Synchronized Sampling Network within the MicroStrain provided desktop software, or the MicroStrain Communication Library (MSCL). Failure to configure the network correctly will lead to wireless packets colliding, resulting in data loss.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x003B;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x03;                    //Payload Length
uint16_t commandId             = 0x003B;                  //Command ID Echo
uint8_t notUsed                = 0x00;                    //RESERVED
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - notUsed]
```

##### Failure Response:
No Response.

<br>


## Initiate Synchronized Sampling (v1, ASPP3)
``ASPP v3.0``

The **Initiate Synchronized Sampling command** is used to put the Node into Synchronized Sampling mode. Once in this mode, the node must receive a beacon from the Base Station to begin sampling and transmitting data packets.

For Synchronized Sampling mode, the wireless sensor network needs to be configured so that each node is assigned an appropriate TDMA slot prior to issuing the Initiate Synchronized Sampling command. To set up the wireless sensor network, use either the Synchronized Sampling Network within the MicroStrain provided desktop software, or the MicroStrain Communication Library (MSCL). Failure to configure the network correctly will lead to wireless packets colliding, resulting in data loss.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x003B;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x003B;                  //Command ID Echo
uint8_t notUsed                = 0x00;                    //RESERVED
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
No Response.

<br>


## Read Single Sensor
``ASPP v1.0``

The **Read Single Sensor** command is used to read the current value of a single channel on the Node.

##### Command:
```cpp
uint8_t commandId              = 0x03;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
uint8_t commandByte            = 0x01;                    //Command Byte
uint8_t channelNumber;                                    //Channel Number
```

##### Success Response:
```cpp
uint8_t commandId              = 0x03;                    //Command ID Echo
uint16_t channelValue;                                    //Value of the Requested Channel
uint16_t checksum;                                        //Checksum of [channelValue]
```

##### Failure Response:
```cpp
uint8_t failId                 = 0x21;                    //Failure Indicator
```

##### Notes:
**Erroneous Data:** Values read using the Read Single Sensor command may be off due to there being no excitation time taken into account. The other full sampling modes use a Sampling Delay, which is an amount of time between sensor excitation power up and A/D sampling.

<br>

## Auto-Balance Channel (v1)
``ASPP v1.0``

The **Auto-Balance Channel** command is used to auto-balance a particular channel on the Node. This command is only applicable to the differential channels on certain Nodes.

##### Command:
```cpp
uint8_t commandId              = 0x62;                    //Command ID
uint16_t nodeAddress;                                     //Node Address
uint8_t channelNumber;                                    //Channel # to Balance
uint16_t targetValue;                                     //Target Balance Value
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
No Response.

##### Failure Response:
No Response.

##### Notes:
**Target Balance Value:** The target balance value represents the desired sensor output value in bits. All differential inputs have a programmable offset feature that allows the user to trim sensor offset (see hardware user manual for more information). This programmable offset can be manually altered via Node EEPROM, or auto-tuned such that the sensor output is balanced to a user-defined target. For example, a common use is to auto-balance to mid-scale (2048 bits) to obtain maximum bipolar dynamic range.

<br>

## Auto-Balance Channel (v2)
``ASPP v1.2``

The **Auto-Balance Channel** command is used to auto-balance a particular channel on the Node. This command is only applicable to the differential channels on certain Nodes.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0065;                  //Command ID
uint8_t channelNumber;                                    //Channel Number to balance
float targetPercentage;                                   //Target Balance Percentage
uint16_t checksum;                                        //Checksum of [stopFlag - targetPercentage]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x10;                    //Payload Length
uint16_t commandId             = 0x0065;                  //Command ID Echo
uint8_t channelNumber;                                    //Channel Number Echo
float targetPercentage;                                   //Target Balance Percentage Echo
uint8_t errorCode;                                        //Error Code
float percentAchieved;                                    //Balance Percentage actually acheived
uint32_t newHardwareOffset;                               //Updated Hardware Offset
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - newHardwareOffset]
```

##### Failure Response:
No Response.

##### Notes:
**Target Balance Percentage:** The percentage desired to balance to. For example, a common use it to auto-balance to mid-scale (50%) to obtain maximum bipolar dynamic range.

**Error Code:** Describes whether the autobalance succeeded or failed.

Code   | Description
-------|--------------
0      | Success
1      | Potentially Bad AutoBalance (values still applied)
2      | Not Supported by the Node
3      | Not Support on the given channel
4      | Target Balance value out of range

**Percent Achieved:** It is not always possible to balance exactly to the requested percentage. The Percentage Achieved gives the result that a successful autobalance actually balanced the channel to.

**Updated Hardware Offset:** The hardware offset value that the channel has been updated to after a successful autobalance.

<br>

## Auto-Balance Channel (v2, ASPP3)
``ASPP v3.0``

The **Auto-Balance Channel** command is used to auto-balance a particular channel on the Node. This command is only applicable to the differential channels on certain Nodes.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0007;                  //Payload Length
uint16_t commandId             = 0x0065;                  //Command ID
uint8_t channelNumber;                                    //Channel Number to balance
float targetPercentage;                                   //Target Balance Percentage
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0010;                  //Payload Length
uint16_t commandId             = 0x0065;                  //Command ID Echo
uint8_t channelNumber;                                    //Channel Number Echo
float targetPercentage;                                   //Target Balance Percentage Echo
uint8_t errorCode;                                        //Error Code
float percentAchieved;                                    //Balance Percentage actually acheived
uint32_t newHardwareOffset;                               //Updated Hardware Offset
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
No Response.

##### Notes:
**Target Balance Percentage:** The percentage desired to balance to. For example, a common use it to auto-balance to mid-scale (50%) to obtain maximum bipolar dynamic range.

**Error Code:** Describes whether the autobalance succeeded or failed.

Code   | Description
-------|--------------
0      | Success
1      | Potentially Bad AutoBalance (values still applied)
2      | Not Supported by the Node
3      | Not Support on the given channel
4      | Target Balance value out of range

**Percent Achieved:** It is not always possible to balance exactly to the requested percentage. The Percentage Achieved gives the result that a successful autobalance actually balanced the channel to.

**Updated Hardware Offset:** The hardware offset value that the channel has been updated to after a successful autobalance.

<br>

## Auto-Calibrate (v1)
``ASPP v1.2``

The **Auto-Calibrate** command is used to auto-calibrate a Node. This command is only applicable to specific Nodes.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen;                                       //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID
// 0 - 116 Specific Command Bytes (varies per device/firmware)
uint16_t checksum;                                        //Checksum of [stopFlag - specific command bytes]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Node Received Response:

The Node sends this packet when it initially received the AutoCal command, before any calibration is performed, to notify the user that calibration is being performed.

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x20;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID Echo
uint8_t status;                                           //Status Code
float timeUntilComplete;                                  //Time Until Completion
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - timeUntilComplete]
```

##### Completion Response:

The Node sends this packet when the AutoCal process has completed and values have been applied to the Node.

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen;                                       //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID Echo
uint8_t completionCode;                                   //Completion Code
// 0 - 113 Completion Info Bytes (varies per device/firmware)
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - completion info bytes]
```

##### Notes:
**Status (Node Received Response):**

Code   | Description
-------|--------------
0      | AutoCal started successfully
1      | Failed to parse the payload of the AutoCal command

**Time Until Completion (node received response):** The amount of time (in seconds) until the AutoCal command will complete, and the AutoCal Success/Fail packet will be sent by the Node. This will be a value of 0 if the Status Flag byte is not 0x00 (indicating the process will not be performed).

**Completion Code (completion response):**

Code   | Description
-------|--------------
0      | Calibration Completed Successfully
1      | Potential invalid calibration (cal still applied)
2      | Potential invalid calibration (cal not applied)


<br>

## Auto-Calibrate (v1, ASPP3)
``ASPP v3.0``

The **Auto-Calibrate** command is used to auto-calibrate a Node. This command is only applicable to specific Nodes.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen;                                      //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID
//Specific Command Bytes (varies per device/firmware)
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Node Received Response:

The Node sends this packet when it initially received the AutoCal command, before any calibration is performed, to notify the user that calibration is being performed.

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x20;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0007;                  //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID Echo
uint8_t status;                                           //Status Code
float timeUntilComplete;                                  //The estimated time for the calibration to complete.
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Completion Response:

The Node sends this packet when the AutoCal process has completed and values have been applied to the Node.

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen;                                      //Payload Length
uint16_t commandId             = 0x0064;                  //Command ID Echo
uint8_t completionCode;                                   //Completion Code
// 0 - 113 Completion Info Bytes (varies per device/firmware)
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Notes:
**Status (Node Received Response):**

Code   | Description
-------|--------------
0      | AutoCal started successfully
1      | Failed to parse the payload of the AutoCal command

**Time Until Completion (node received response):** The amount of time (in seconds) until the AutoCal command will complete, and the AutoCal Success/Fail packet will be sent by the Node. This will be a value of 0 if the Status Flag byte is not 0x00 (indicating the process will not be performed).

**Completion Code (completion response):**

Code   | Description
-------|--------------
0      | Calibration Completed Successfully
1      | Potential invalid calibration (cal still applied)
2      | Potential invalid calibration (cal not applied)


---

##### SHM-Link-2 Specifics

**Command Bytes:** None

**Completion Info Bytes:**

```cpp
uint8_t ch1Error;                                         //Channel 1 Error Code
float ch1Offset;                                          //Channel 1 Offset
uint8_t ch2Error;                                         //Channel 2 Error Code
float ch2Offset;                                          //Channel 2 Offset
uint8_t ch3Error;                                         //Channel 3 Error Code
float ch3Offset;                                          //Channel 3 Offset
float temperature;                                        //Temperature (Celsius) at time of cal
```

**Channel Error Codes:**

Code   | Description
-------|--------------
0      | No Error
1      | Sensor not plugged in
2      | Sensor shorted
3      | Invalid Sensor input


---

##### SHM-Link-201 Shunt Cal Specifics

**Command Bytes:** None

**Completion Info Bytes:**

```cpp
uint8_t ch1Error;                                         //Channel 1 Error Code
float ch1Slope;                                           //Channel 1 Slope
float ch1Offset;                                          //Channel 1 Offset
uint8_t ch2Error;                                         //Channel 2 Error Code
float ch2Slope;                                           //Channel 2 Slope
float ch2Offset;                                          //Channel 2 Offset
uint8_t ch3Error;                                         //Channel 3 Error Code
float ch3Slope;                                           //Channel 3 Slope
float ch3Offset;                                          //Channel 3 Offset
float temperature;                                        //Temperature (Celsius) at time of cal
```

**Channel Error Codes:**

Code   | Description
-------|--------------
0      | No Error
4      | The baseline data may have railed high.
5      | The baseline data may have railed low.
6      | The shunted data may have railed high.
7      | The shunted data may have railed low.
8      | There was an unexpected slope to the data.
9      | No shunt was detected in the data.
10     | A timeout has occurred.


---

##### Shunt Cal Specifics (V-Link-200)

**Command Bytes:**

```cpp
uint8_t channelNumber;                                    //The channel to calibrate (1 = ch1)
uint8_t hardwareGain;                                     //The Hardware Gain to use in the autocal operation
uint16_t hardwareOffset;                                  //The Hardware Offset to use in the autocal operation
uint8_t numActiveGauges;                                  //The number of active gauges to use in the autocal operation
uint16_t gaugeResistance;                                 //The gauge resistance to use in the autocal operation
uint16_t shuntResistance;                                 //The shunt resistance to use in the autocal operation
float gaugeFactor;                                        //The gauge factor to use in the autocal operation
```

**Completion Info Bytes:**

```cpp
uint8_t channelNumber;              //Channel number echo
uint8_t channelError;               //Channel Error Code
float slope;                        //Calculated slope that can be applied (not auto applied)
float offset;                       //Calculated offset that can be applied (not auto applied)
float baseMedian;                   //The median of the baseline data sampled during the shunt calibration.
float baseMin;                      //The minimum of the baseline data sampled during the shunt calibration.
float baseMax;                      //The maximum of the baseline data sampled during the shunt calibration.
float shuntMedian;                  //The median of the shunted data sampled during the shunt calibration.
float shuntMin;                     //The minimum of the shunted data sampled during the shunt calibration.
float shuntMax;                     //The maximum of the shunted data sampled during the shunt calibration.
```

**Channel Error Flags:**

Code   | Description
-------|--------------
0      | No Error
3      | Unsupported Channel
4      | The baseline data may have railed high.
5      | The baseline data may have railed low.
6      | The shunted data may have railed high.
7      | The shunted data may have railed low.
8      | There was an unexpected slope to the data.
9      | No shunt was detected in the data.
10      | A timeout has occurred.


<br>

## Log Session Info (v1)
``ASPP v1.4``

The **Log Session Info** command retrieves datalogging information about the Node.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x0C;                    //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID Echo
uint16_t sessionCount;                                    //Total number of sessions logged on the Node
uint32_t startAddress;                                    //Flash Address of the first log header
uint32_t size;                                            //Max number of logged bytes
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - size]
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x03;                    //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID Echo
uint8_t status;                                           //1 = flash busy
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - status]
```

<br>

## Log Session Info (v1, ASPP3)
``ASPP v3.0``

The **Log Session Info** command retrieves datalogging information about the Node.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x000C;                  //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID Echo
uint16_t sessionCount;                                    //Total number of sessions logged on the Node
uint32_t startAddress;                                    //Flash Address of the first log header
uint32_t size;                                            //Max number of logged bytes
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0040;                  //Command ID Echo
uint8_t status;                                           //1 = flash busy
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

<br>

## Erase Logged Data (v2)
``ASPP v1.4``

The **Erase Logged Data** command is used to erase all sampled data stored on the Node's memory. This cannot be undone.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID Echo
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x03;                    //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID Echo
uint8_t status;                                           //1 = flash busy
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - status]
```

<br>

## Erase Logged Data (v2, ASPP3)
``ASPP v3.0``

The **Erase Logged Data** command is used to erase all sampled data stored on the Node's memory. This cannot be undone.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID Echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0042;                  //Command ID Echo
uint8_t status;                                           //1 = flash busy
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

<br>

## Get Logged Data (v1)
``ASPP v1.4``

The **Get Logged Data** command is used to download sampled data stored on the Node's memory.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x06;                    //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID
uint32_t address;                                         //Flash Address to read
uint16_t checksum;                                        //Checksum of [stopFlag - address]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x6C;                    //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID Echo
uint32_t address;                                         //Flash Address of first byte downloaded
uint8_t data[102];                                        //Data read from flash
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - data]
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID Echo
uint32_t address;                                         //Flash Address of first byte downloaded
uint8_t status;                                           //1 = flash busy
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - status]
```

See [Get Logged Data (v2) for logged data format details](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/Commands.md#logged-data-format).

<br>

## Get Logged Data (v1, ASPP3)
``ASPP v3.0``

The **Get Logged Data** command is used to download sampled data stored on the Node's memory.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0006;                  //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID
uint32_t address;                                         //Flash Address to read
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x006C;                  //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID Echo
uint32_t address;                                         //Flash Address of first byte downloaded
uint8_t data[102];                                        //Data read from flash
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Error Response:

```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x02;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x07;                    //Payload Length
uint16_t commandId             = 0x0041;                  //Command ID Echo
uint32_t address;                                         //Flash Address of first byte downloaded
uint8_t status;                                           //1 = flash busy
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

#### Logged Data Format

Data stored in flash is always preceded by a block header, a refresh header, or a session change header. Block headers are written at the start of each flash block. Refresh headers are written after data associated with a block header is written, when no parameters have changed, and a new flash block hasn't been reached. Session change headers are written when either the timestamp or session index has changed and a new flash block hasn't been reached. If there is not enough room at the end of the flash block to store the next chunk of data the logging algorithm will move to the next block, writing a block header with the data, and leaving the rest of the previous block erased (0xFF in the case of most nodes). All header fields are encoded in node endianness (little endian in the case of most nodes).

##### Example

Flash Index  | Value
-------------|--------------
0 |	Block header for 42 sweeps of data
46 |	Data as described in block header
298 |	Refresh header for 42 sweeps of data
301 |	Data as described in refresh header
553 |	Refresh header for 42 sweeps of data
556 |	…
65536 |	Block header due to new flash block
65582 |	Block header data
65834 |	Refresh header
65837 |	…
69000 |	Session change header due to bad sweep (timestamp out of sync)
69012 |	Session change header data

##### Session

A logging session is defined as a contiguous section of logged data. A new session occurs when the user starts a logged data session, each time there is a burst of data (when burst logging), or when a data event occurs and the node starts logging to when events cease and data stops logging (with data driven logging). The session index starts at 0 or the highest logged session index if there are logged sessions.

##### Checksum

Each logging packet (header + data) contains a 16 bit fletcher checksum at the end of the data. The checksum encompasses all bytes in the packet before the checksum (up to and including the header id).


##### Block Header 

There are multiple versions of block headers. The version of the block header is contained in the block header itself, and determines how the header should be parsed.

###### Block Header version 0

```cpp
// cal data exactly as it is in eeprom, no padding between values
struct CalData
{
  uint8_t equationId;
  uint8_t unitId;
  float slope;
  float offset;
}
 
uint8_t id = 0xBB;              // block header id
uint8_t version = 0;            // version number of the block header
uint8_t headerSize;             // number of bytes between this field and the start of data
uint8_t sweepCount;             // number of sweeps that follow the header
uint16_t index;                 // incremented every block
uint16_t sessionIndex;          // incremented for every new logging session
uint64_t timestamp;             // timestamp of the first following sweep in nanoseconds since 1970
uint8_t sampleRate;             // ASPP sample rate identifier
uint16_t channelMask;           // bit mask of logged channels
uint8_t dataType;               // ASPP data type identifier
CalData calData[numChannels];   // Calibration data for each channel (numChannels is hamming weight of channelMask)
```

###### Block Header version 1

```cpp
// cal data exactly as it is in eeprom, no padding between values
struct CalData
{
  uint8_t equationId;
  uint8_t unitId;
  float slope;
  float offset;
}

struct AlgorithmMeta
{
  uint8_t algorithmId;
  uint16_t channelMask;
}
 
uint8_t id = 0xBB;              // block header id
uint8_t version = 1;            // version number of the block header
uint8_t headerSize;             // number of bytes between this field and the start of data
uint8_t sweepCount;             // number of sweeps that follow the header
uint8_t sweepType;              // type of sweeps that follow the header: 0 for normal data, 1 for math data
uint16_t index;                 // incremented every block
uint16_t sessionIndex;          // incremented for every new logging session
uint64_t timestamp;             // timestamp of the first following sweep in nanoseconds since 1970
uint8_t sampleRate;             // ASPP sample rate identifier
uint16_t channelMask;           // bit mask of logged channels
uint8_t dataType;               // ASPP data type identifier
uint8_t numActiveAlgorithms;    // Number of algorithms being used
uint32_t calculationRate;       // Rate at which processed data was sampled
CalData calData[numChannels];   // Calibration data for each channel (numChannels is hamming weight of channelMask)
AlgorithmMeta algorithmMeta[numActiveAlgorithms];  // Meta information about used algorithms
```

The `calculationRate` is the rate at which the calculated channels are determined. This field relative to the sample rate of the raw data defines the window of raw samples from which the calculation is made. The calculation rate is encoded as a unsigned 32 bit number with the most significant bit designating hertz, 1, or seconds, 0, and the 31 least significant bits designating the sample rate value. For example:
```
0x8000001C = 28 Hz
0x0000001C = 28 Seconds
```

##### Refresh Header

```cpp
uint8_t id = 0xBA;     // refresh header id
uint8_t sweepCount;    // number of sweeps that follow the header
```

##### Session Change Header

There are multiple versions of the Session Change Header. The session change header id can be used to identify the version and how the header should be parsed:

###### Session Change Header version 0 (0xBC)

```cpp
uint8_t id = 0xBC;       // session change header id
uint8_t sweepCount;      // number of sweeps that follow the header
uint64_t timestamp;      // timestamp of first sweep following the header
uint16_t sessionIndex;   // index of the session the data following the header belongs to
```

###### Session Change Header version 1 (0xBD)

```cpp
uint8_t id = 0xBD;       // session change header id
uint8_t sweepCount;      // number of sweeps that follow the header
uint8_t sweepType;       // type of sweeps that follow the header: 0 for normal data, 1 for math data
uint64_t timestamp;      // timestamp of first sweep following the header
uint16_t sessionIndex;   // index of the session the data following the header belongs to
```

<br>

## Get Diagnostic Info (v1)
``ASPP v1.5``

The **Get Diagnostic Info** command is used to get diagnostic information about the Wireless Node. Note that a Node can also be configured to send a [Diagnostic data packet](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/Data%20Packets.md#diagnostic-packet) at a specific interval as well. The information in the data packet is the same as in the response for this command.

##### Command:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x05;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen             = 0x02;                    //Payload Length
uint16_t commandId             = 0x0009;                  //Command ID
uint16_t checksum;                                        //Checksum of [stopFlag - commandId]
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAA;                    //Start of Packet Byte
uint8_t stopFlag               = 0x07;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint16_t nodeAddress;                                     //Node Address
uint8_t payloadLen;                                       //Payload Length
uint16_t commandId             = 0x0009;                  //Command ID Echo
uint8_t info1Len;                                         //Info Item 1 Length
uint8_t info1Id;                                          //Info Item 1 ID
uint8_t | uint16_t | uint32_t info1Val;                   //Info Item 1 Value
//Repeat Into Item Length, ID, and Value for all the Info Items in the packet
int8_t nodeRssi;                                          //Node RSSI
int8_t baseRssi;                                          //Base Station RSSI
uint16_t checksum;                                        //Checksum of [stopFlag - info item bytes]
```

##### Failure Response:
none

For more information on the payload of this packet, see the documentation for the [Diagnostic Data Packet](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/Data%20Packets.md#diagnostic-packet).

<br>

## Get Diagnostic Info (v1, ASPP3)
``ASPP v3.0``

The **Get Diagnostic Info** command is used to get diagnostic information about the Wireless Node. Note that a Node can also be configured to send a [Diagnostic data packet](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/Data%20Packets.md#diagnostic-packet) at a specific interval as well. The information in the data packet is the same as in the response for this command.

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0002;                  //Payload Length
uint16_t commandId             = 0x0009;                  //Command ID
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen;                                      //Payload Length
uint16_t commandId             = 0x0009;                  //Command ID Echo
uint8_t info1Len;                                         //Info Item 1 Length
uint8_t info1Id;                                          //Info Item 1 ID
uint8_t | uint16_t | uint32_t info1Val;                   //Info Item 1 Value
//Repeat Into Item Length, ID, and Value for all the Info Items in the packet
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
none

For more information on the payload of this packet, see the documentation for the [Diagnostic Data Packet](https://github.com/LORD-MicroStrain/Protocols/blob/master/Wireless/Data%20Packets.md#diagnostic-packet).

<br>

## Cycle Power & Radio (v1)
``ASPP v1.0``

To cycle the power on the Node, use the `Write EEPROM` command and write a `1` to `EEPROM 250`.

To cycle the radio on the Node, use the `Write EEPROM` command and write a `2` to `EEPROM 250`.

<br>

## Cycle Power & Radio (v1, ASPP3)
``ASPP v3.0``

##### Command:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x04;                    //Delivery Stop Flag
uint8_t appDataType            = 0x00;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0031;                  //Command ID
uint8_t resetType;                                        //Reset Type (1 = hard reset, 2 = soft reset)
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint8_t RESERVED               = 0x7F;                    //Reserved Byte
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Base Station Received Response
See [Base Station Received Response documentation](#base-station-received-response)

##### Success Response:
```cpp
uint8_t startByte              = 0xAC;                    //Start of Packet Byte
uint8_t stopFlag               = 0x08;                    //Delivery Stop Flag
uint8_t appDataType            = 0x22;                    //App Data Type
uint32_t nodeAddress;                                     //Node Address
uint16_t payloadLen            = 0x0003;                  //Payload Length
uint16_t commandId             = 0x0031;                  //Command ID Echo
uint8_t resetType;                                        //Reset Type Echo
uint8_t nodeRssi;                                         //Node RSSI
uint8_t baseRssi;                                         //Base Station RSSI
uint32_t checksum;                                        //CRC Checksum of all bytes
```

##### Failure Response:
none

