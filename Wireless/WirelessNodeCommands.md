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

<br>
## Write Node EEPROM

The **Write Node EEPROM** command is used to write a value to a specific memory address on the Node's EEPROM.

See the Node EEPROM Map for specific memory address details.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x05;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x06;		//Payload Length
uint16_t commandId 		= 0x0004;	//Command ID
uint16_t eepromAddress;				//EEPROM Address to Write to
uint16_t value;						//Value to Write to EEPROM
uint16_t checksum;					//Checksum of [stopFlag - value]
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
uint16_t commandId		= 0x0004;	//Command ID Echo
int8_t notUsed;						//RESERVED
int8_t baseRssi;					//Base RSSI
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Failure Response:
No Response.

<br>
## Initiate Sleep Mode

The **Initiate Sleep Mode** command is used to put the Node in a low power state. When the Node is in this low power Sleep Mode, it will not hear any commands except for the Set to Idle command, which will wake the node and put it back into its normal, idle state. The Node should be put into Sleep Mode when
you no longer needs to communicate with the node, but want to keep it powered on and preserve battery life. 

##### Command:
```cpp
uint8_t commandId 		= 0x32;		//Command ID
uint16_t nodeAddress;				//Node Address
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
## Set to Idle

The **Set to Idle** command is used to put a Node that is sampling, or sleeping, back into the Idle Mode so that it may be communicated with.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0xFE;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t commandId 		= 0x0090;	//Command ID
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Initial Response:
An initial response comes directly from the Base Station to acknowledge that the command was received by the Base Station and sent to the Node.
```cpp
uint8_t packetSentAck 	= 0xAA;		//Package Sent Acknowledgement
```

##### Success Response:
The Node was set to idle and can now be communicated with.
```cpp
uint8_t commandId 		= 0x90;		//Command ID Echo
uint8_t commandCeased 	= 0x01;		//The Set to Idle command has ceased
```

##### Failure Response:
The Set to Idle process was aborted.
```cpp
uint8_t failId 			= 0x21;		//Failed/Aborted ID
uint8_t commandCeased 	= 0x01;		//The Set to Idle command has ceased
```

##### Notes:
**Ongoing Operation:** The Set to Idle command puts the Base Station in a mode that sends small packets as fast as possible in an attempt to communicate with the Node. The Base Station will periodically check to see if the Node has responded to a ping request. The function will continue indefinitely until either the Node responds, or the user sends any byte to the Base Station, which cancels the operation. No incoming packets will be heard while the Base Station is in this mode.

**Broadcast Special Case:** When the broadcast Node address 65535 (0xFFFF) is used, the Base Station does not check for a ping response. It will continue sending the stop Node command until interrupted by the user (any single byte sent to the Base Station). This will attempt to stop all Nodes on the current frequency that the Base Station is on.
