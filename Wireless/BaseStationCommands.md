# Base Station Commands

**List of Commands:**

####ASPP v1.0
* [Ping Base Station (v1)](#ping-base-station-v1)
* [Read EEPROM (v1)](#read-base-station-eeprom-v1)
* [Write EEPROM (v1)](#write-base-station-eeprom-v1)
* [Enable Beacon (v1)](#enable-beacon-v1)
* [Disable Beacon (v1)](#disable-beacon-v1)

####ASPP v1.1
(BaseStation firmware 4.0+)
* [Ping Base Station (v2)](#ping-base-station-v2)
* [Read EEPROM (v2)](#read-base-station-eeprom-v2)
* [Write EEPROM (v2)](#write-base-station-eeprom-v2)
* [Enable Beacon (v2)](#enable-beacon-v2)
* [Disable Beacon (v2)](#disable-beacon-v2)

## Ping Base Station (v1)

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
```cpp
uint8_t commandId = 0x01;	//Command ID
```

##### Success Response:
```cpp
uint8_t commandId = 0x01;	//Command ID Echo
```

##### Failure Response:
None.

<br>
## Ping Base Station (v2)

The **Ping Base Station** command is used to ensure that the host computer and the Base Station are properly communicating.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x0E;		//Delivery Stop Flag
uint8_t appDataType 	= 0x30;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x02;		//Payload Length
uint16_t commandId		= 0x0001;	//Command ID
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x31;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x02;		//Payload Length
uint16_t commandId		= 0x0001;	//Command ID Echo
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Failure Response:
None.

<br>
## Read Base Station EEPROM (v1)

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t commandId 		= 0x73;		//Command ID
uint16_t eepromAddress;				//EEPROM address to read
uint16_t checksum;					//Checksum of [eepromAddress]
```

##### Success Response:
```cpp
uint8_t commandId 		= 0x73;		//Command ID Echo
uint16_t value;						//Value read from EEPROM
uint16_t checksum;					//Checksum of [value]
```

##### Fail Response:
```cpp
uint8_t failId 			= 0x21;		//Fail ID
```

<br>
## Read Base Station EEPROM (v2)

The **Read Base Station EEPROM** command is used to read the value of a specific memory address from the Base Station's EEPROM.  

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x0E;		//Delivery Stop Flag
uint8_t appDataType 	= 0x30;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x04;		//Payload Length
uint16_t commandId		= 0x0073;	//Command ID
uint16_t eepromAddress;				//EEPROM Address to Read
uint16_t checksum;					//Checksum of [stopFlag - eepromAddress]
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x31;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x06;		//Payload Length
uint16_t commandId		= 0x0073;	//Command ID Echo
uint16_t eepromAddress;				//EEPROM Address Read
uint16_t value;						//Value Read from EEPROM
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - value]
```

##### Fail Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x32;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x05;		//Payload Length
uint16_t commandId		= 0x0073;	//Command ID Echo
uint16_t eepromAddress;				//EEPROM Address Attempted to Read
uint8_t errorCode;					//Error Code
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - errorCode]
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
uint8_t commandId 		= 0x78;		//Command ID
uint16_t eepromAddress;				//EEPROM address to write to
uint16_t value;						//Value to write to EEPROM
uint16_t checksum;					//Checksum of [eepromAddress - value]
```

##### Success Response:
```cpp
uint8_t commandId 		= 0x78;		//Command ID Echo
uint16_t value;						//Value written to EEPROM
uint16_t checksum;					//Checksum of [value]
```

##### Fail Response:
```cpp
uint8_t failId 			= 0x21;		//Fail ID
```

<br>
## Write Base Station EEPROM (v2)

The **Write Base Station EEPROM** command is used to write a value to a specific memory address on the Base Station's EEPROM.

See the Base Station EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x0E;		//Delivery Stop Flag
uint8_t appDataType 	= 0x30;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x06;		//Payload Length
uint16_t commandId		= 0x0078;	//Command ID
uint16_t eepromAddress;				//EEPROM Address to Write to
uint16_t value;						//Value to Write to EEPROM
uint16_t checksum;					//Checksum of [stopFlag - value]
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x31;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x06;		//Payload Length
uint16_t commandId		= 0x0078;	//Command ID Echo
uint16_t eepromAddress;				//EEPROM Address Written to
uint16_t value;						//Value Written
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - value]
```

##### Fail Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x32;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x07;		//Payload Length
uint16_t commandId		= 0x0078;	//Command ID Echo
uint16_t eepromAddress;				//EEPROM Address Attempted to Write
uint16_t value;						//Value Attempted to Write
uint8_t errorCode;					//Error Code
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - errorCode]
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
uint16_t commandId 			= 0xBEAC;		//Command ID
uint32_t timestamp;							//Timestamp to give to the Beacon
```

##### Success Response:
```cpp
uint16_t commandId 			= 0xBEAC;		//Command ID Echo
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
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x0E;		//Delivery Stop Flag
uint8_t appDataType 	= 0x30;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x06;		//Payload Length
uint16_t commandId		= 0xBEAC;	//Command ID
uint32_t timestamp;					//Timestamp to give to the Beacon
uint16_t checksum;					//Checksum of [stopFlag - timestamp]
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x31;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x06;		//Payload Length
uint16_t commandId		= 0xBEAC;	//Command ID Echo
uint32_t timestamp;					//Timestamp given to the Beacon
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - timestamp]
```

##### Fail Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x32;		//App Data Type
uint16_t baseAddress	= 0x1234;	//Base Station Address
uint8_t payloadLen		= 0x07;		//Payload Length
uint16_t commandId		= 0xBEAC;	//Command ID Echo
uint32_t timestamp;					//Timestamp Attempted to Set
uint8_t errorCode;					//Error Code
uint8_t RESERVED;					//Reserved Byte
uint8_t RESERVED;					//Reserved Byte
uint16_t checksum;					//Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description 
-------------|-------------- 
4            | Hardware Error

<br>
## Disable Beacon (v1)

The Disable Beacon command is used to turn off the beacon on the Base Station.

##### Command:
```cpp
uint16_t commandId 			= 0xBEAC;		//Command ID
uint32_t disableBeacon 		= 0xFFFFFFFF;	//Value to disable the beacon
```

##### Success Response:
```cpp
uint16_t commandId 			= 0xBEAC;		//Command ID Echo
```
##### Fail Response:
None.

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.

<br>
## Disable Beacon (v2)

The Disable Beacon command is used to turn off the beacon on the Base Station.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;			//Start of Packet byte
uint8_t stopFlag 		= 0x0E;			//Delivery Stop Flag
uint8_t appDataType 	= 0x30;			//App Data Type
uint16_t baseAddress	= 0x1234;		//Base Station Address
uint8_t payloadLen		= 0x06;			//Payload Length
uint16_t commandId		= 0xBEAC;		//Command ID
uint32_t disableBeacon	= 0xFFFFFFFF;	//Value to Disable the Beacon
uint16_t checksum;						//Checksum of [stopFlag - timestamp]
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;			//Start of Packet byte
uint8_t stopFlag 		= 0x07;			//Delivery Stop Flag
uint8_t appDataType 	= 0x31;			//App Data Type
uint16_t baseAddress	= 0x1234;		//Base Station Address
uint8_t payloadLen		= 0x06;			//Payload Length
uint16_t commandId		= 0xBEAC;		//Command ID Echo
uint32_t disableBeacon	= 0xFFFFFFFF;	//Value to Disable the Beacon
uint8_t RESERVED;						//Reserved Byte
uint8_t RESERVED;						//Reserved Byte
uint16_t checksum;						//Checksum of [stopFlag - timestamp]
```

##### Fail Response:
```cpp
uint8_t startByte 		= 0xAA;			//Start of Packet byte
uint8_t stopFlag 		= 0x07;			//Delivery Stop Flag
uint8_t appDataType 	= 0x32;			//App Data Type
uint16_t baseAddress	= 0x1234;		//Base Station Address
uint8_t payloadLen		= 0x07;			//Payload Length
uint16_t commandId		= 0xBEAC;		//Command ID Echo
uint32_t disableBeacon	= 0xFFFFFFFF;	//Value to Disable the Beacon
uint8_t errorCode;						//Error Code
uint8_t RESERVED;						//Reserved Byte
uint8_t RESERVED;						//Reserved Byte
uint16_t checksum;						//Checksum of [stopFlag - errorCode]
```
**Error Codes:**

Code         | Description 
-------------|-------------- 
4            | Hardware Error

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.
