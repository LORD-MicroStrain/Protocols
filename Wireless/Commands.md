# Wireless Node and Base Station Commands

Note that some commands are device specific.

New devices/firmware support `Eeprom 124`, which identifies the ASPP version (msb.lsb) that the device supports.
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

#### Base Station Commands

Command      | Command ID    |  Base Station ASPP Version required
-------------|---------------|--------------------
[Start RF Sweep Mode](#start-rf-sweep-mode) | 0x00ED | ASPP v1.3
[Ping Base Station (v2)](#ping-base-station-v2) | 0x0001 | ASPP v1.1
[Ping Base Station (v1)](#ping-base-station-v1) | 0x01 | ASPP v1.0
[Read Base Station EEPROM (v2)](#read-base-station-eeprom-v2) | 0x0073 | ASPP v1.1
[Read Base Station EEPROM (v1)](#read-base-station-eeprom-v1) | 0x73 | ASPP v1.0
[Write Base Station EEPROM (v2)](#write-base-station-eeprom-v2) | 0x0078 | ASPP v1.1
[Write Base Station EEPROM (v1)](#write-base-station-eeprom-v1) | 0x78 | ASPP v1.0
[Enable Beacon (v2)](#enable-beacon-v2) | 0xBEAC | ASPP v1.1
[Enable Beacon (v1)](#enable-beacon-v1) | 0xBEAC | ASPP v1.0
[Disable Beacon (v2)](#disable-beacon-v2) | 0xBEAC | ASPP v1.1
[Disable Beacon (v1)](#disable-beacon-v1) | 0xBEAC | ASPP v1.0
[Beacon Status](#beacon-status) | 0xBEAD | ASPP v1.1
[Cycle Power & Radio](#cycle-power--radio) | - | ASPP v1.0


#### Node Commands

Command      | Command ID    |  Node ASPP Version required
-------------|---------------|--------------------
[Quick Ping (v2)](#short-ping-v2) | 0x0012 | ASPP v1.2
[Quick Ping (v1)](#short-ping-v1) | 0x02 | ASPP v1.0
[Detailed Ping](#long-ping) | 0x0002 | ASPP v1.0
[Initiate Sleep Mode](#initiate-sleep-mode) | 0x32 | ASPP v1.0
[Set to Idle](#set-to-idle) | 0x0090 | ASPP v1.0
[Read EEPROM (v2)](#read-node-eeprom-v2) | 0x0007 | ASPP v1.1
[Read EEPROM (v1)](#read-node-eeprom-v1) | 0x0003 | ASPP v1.0
[Write EEPROM (v2)](#write-node-eeprom-v2) | 0x0008 | ASPP v1.1
[Write EEPROM (v1)](#write-node-eeprom-v1) | 0x0004 | ASPP v1.0
[Initiate Synchronized Sampling](#initiate-synchronized-sampling) | 0x003B | ASPP v1.0
[Initiate Low Duty Cycle (v2)](#initiate-low-duty-cycle-v2) | 0x0039 | ASPP v1.5
[Initiate Low Duty Cycle (v1)](#initiate-low-duty-cycle-v1) | 0x0038 | ASPP v1.0
[Initiate Legacy Streaming](#initiate-real-time-streaming-legacy) | 0x38 | ASPP v1.0
[Arm for Datalogging](#arm-node-for-datalogging) | 0x000D | ASPP v1.0
[Trigger Armed Datalogging](#trigger-armed-datalogging) | 0x000E | ASPP v1.0
[Get Logged Data](#get-logged-data) | 0x0041 | ASPP v1.4
[Page Download](#page-download) | 0x05 | ASPP v1.0
[Log Session Info](#log-session-info) | 0x0040 | ASPP v1.4
[Erase Logged Data (v2)](#erase-logged-data-v2) | 0x0042 | ASPP v1.4
[Erase Logged Data (v1)](#erase-logged-data) | 0x06 | ASPP v1.0
[Auto-Balance Channel (v2)](#auto-balance-channel-v2) | 0x0065 | ASPP v1.2
[Auto-Balance Channel (v1)](#auto-balance-channel-v1) | 0x62 | ASPP v1.0
[Auto-Calibrate](#auto-calibrate) | 0x0064 | ASPP v1.2
[Get Diagnostic Info](#get-diagnostic-info) | 0x0009 | ASPP v1.5
[Read Single Sensor](#read-single-sensor) | 0x03 | ASPP v1.0
[Cycle Power & Radio](#cycle-power--radio) | - | ASPP v1.0

## Ping Base Station (v1)

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
## Read Base Station EEPROM (v1)

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
## Write Base Station EEPROM (v1)

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
## Enable Beacon (v1)

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
## Disable Beacon (v1)

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
## Beacon Status

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
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
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
## Start RF Sweep Mode

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
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
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
uint16_t checksum;                       //Checksum of [stopFlag - timestamp]
```

##### Notes:

If the device cannot support the requested parameters, they will be clamped to the closest valid value.
The data packets will relect such changes.


<br>
## Cycle Power & Radio

To cycle the power on the device, use the `Write EEPROM` command and write a `1` to `EEPROM 250`.

To cycle the radio on the device, use the `Write EEPROM` command and write a `2` to `EEPROM 250`.
