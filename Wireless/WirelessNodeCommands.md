# Wireless Node Commands


## Short Ping

The **Short Ping** command is used to check the communication between the Base Station and the Node. This command has a direct success/fail response, so it can immediately tell you whether communication was successful. Other commands,do not have a fail response, requiring you to use a timeout to determine a failure.

##### Command:
```cpp
uint8_t commandId = 0x02;	//Command ID
uint16_t nodeAddress;		//Node Address
```

##### Success Response:
```cpp
uint8_t commandId = 0x02;	//Command ID Echo
```

##### Failure Response:
```cpp
uint8_t failId = 0x21;		//Failure ID
```

<br>
## Long Ping

The **Long Ping** command is used to check the communication between the Base Station and the Node, and gives more information than the Short Ping command.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x05;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t commandId 		= 0x0002;	//Command ID
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Initial Response:
An initial response comes directly from the Base Station to acknowledge that the command was received by the Base Station and sent to the Node.
```cpp
uint8_t packetSentAck 	= 0xAA;		//Package Sent Acknowledgement
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x07;		//Delivery Stop Flag
uint8_t appDataType 	= 0x02;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t notUsed 		= 0x0000;	//Empty Payload (not used)
int8_t nodeRssi;					//Node RSSI
int8_t baseRssi;					//Base RSSI
uint16_t checksum;					//Checksum of [stopFlag - notUsed]
```

##### Failure Response:
No Response.

<br>
## Read Node EEPROM

The **Read Node EEPROM** command is used to read the value of a specific memory address from the Node's EEPROM. 

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x05;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x04;		//Payload Length
uint16_t commandId 		= 0x0003;	//Command ID
uint16_t eepromAddress;				//EEPROM Address to Read
uint16_t checksum;					//Checksum of [stopFlag - eepromAddress]
```

##### Initial Response:
An initial response comes directly from the Base Station to acknowledge that the command was received by the Base Station and sent to the Node.
```cpp
uint8_t packetSentAck 	= 0xAA;		//Package Sent Acknowledgement
```

##### Success Response:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x00;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t eepromVal;					//Value Read from EEPROM
int8_t notUsed;						//RESERVED
int8_t baseRssi;					//Base RSSI
uint16_t checksum;					//Checksum of [stopFlag - eepromVal]
```

##### Failure Response:
No Response.
