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
int8_t baseRssi;					//Base Station RSSI
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
int8_t baseRssi;					//Base Station RSSI
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

<br>
## Arm Node for Datalogging

Use the **Arm Node** command to put the node in an armed state waiting for the [Trigger Armed Datalogging](#trigger-armed-datalogging) command.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;						//Start of Packet Byte
uint8_t stopFlag 		= 0x05;						//Delivery Stop Flag
uint8_t appDataType 	= 0x00;						//App Data Type
uint16_t nodeAddress;								//Node Address
uint8_t payloadLen 		= 0x02 + # of user bytes;	//Payload Length
uint16_t commandId 		= 0x000D;					//Command ID
int8_t userBytes[0-50];								//up to 50 (optional) user entered bytes
uint16_t checksum;									//Checksum of [stopFlag - userBytes]
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
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x03;		//Payload Length
uint16_t commandId		= 0x000D;	//Command ID Echo
uint8_t reserved1;					//RESERVED
int8_t reserved2;					//RESERVED
int8_t baseRssi;					//Base Station RSSI
uint16_t checksum;					//Checksum of [stopFlag - reserved1]
```

##### Failure Response:
No Response.

##### Notes:
**User Entered Bytes:** You may send up to 50 bytes with the Arm Command which will then be in the header information of the packet when the data is downloaded from the node using the [Page Download](#page-download) command.

**Disarming:** A Node will stay in this armed state for a default of 10 seconds (EEPROM adjustable). To disarm an Armed Node manually, use the [Set to Idle](#set-to-idle) command.

<br>
## Trigger Armed Datalogging

The **Trigger Armed Datalogging** command is used to initiate a data capture session on-board the Node.The data will be stored in the Node's internal memory and may be downloaded at a later time. 

In most cases, you will want to [Arm](#arm-node-for-datalogging) each Node individually, and then send this command to the broadcast Node Address (65535 or 0xFFFF). This will be sent to all nodes on the Base Station's operating frequency, and any Nodes that are in the "Armed" state will start datalogging. This can be useful to start datalogging on multiple nodes at the same time.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;			//Start of Packet Byte
uint8_t stopFlag 		= 0x05;			//Delivery Stop Flag
uint8_t appDataType 	= 0x00;			//App Data Type
uint16_t nodeAddress;					//Node Address
uint8_t payloadLen 		= 0x0A;			//Payload Length
uint16_t commandId 		= 0x000E;		//Command ID
uint32_t timestampSec;					//UTC Timestamp (Seconds)
uint32_t timestampNano;					//UTC Timestamp (Nanoseconds)
uint16_t checksum;						//Checksum of [stopFlag - timestampNano]
```

##### Success Response:
No Response.

##### Failure Response:
No Response.

##### Notes:
**Timestamp:** The Timestamp is made up of 2 values, each of which are 4 bytes. The first value represents the seconds of the timestamp, and the second value represents the nanoseconds of the timestamp. When downloading the logged data from the node, this timestamp will be transmitted in the header information and can be used to determine the exact timestamp of each data point. These bytes represent the current UTC time in seconds from the Unix Epoch (January 1, 1970).

<br>
## Page Download

The **Page Download** command is used to retrieve a logged data session from the Node. Note that it can also be used to read large chunks of EEPROM values as well.

##### Command:
```cpp
uint8_t commandId = 0x05;		//Command ID
uint16_t nodeAddress;			//Node Address
uint16_t pageIndex;				//Index of Page to download
```

##### Success Response:
```cpp
uint8_t commandId = 0x05;		//Command ID Echo
uint8_t data[264];				//The Page Data (132 2-byte values)
uint16_t checksum;				//Checksum of [data]
```

##### Failure Response:
```cpp
uint8_t commandId = 0x05;		//Command ID Echo
uint16_t failId = 0x21;			//Fail Indicator
```

##### Notes:
**Page Index:** Each Node contains 2MB of memory. These 2MB are mapped to 8192 pages of data, with each page containing 264 bytes. 

Pages are numbered sequentially from 0 to 8191:

* **Page 0** contains data points that represent the value in the Node's EEPROM from locations 0 - 254.
* **Page 1** contains data points that represent the value in the Node's EEPROM from locations 256 - 510.
* **Page 2** is the first page that will contain sampled data that was logged to the node. 

**Data Sessions:** A Node can contain multiple consecutive datalogging sessions. Each of these sessions has a leading multi-byte header which is used to identify the start of a new datalogging session and the end of the previous session. The header contains the datalogging information stored during that particular session.
