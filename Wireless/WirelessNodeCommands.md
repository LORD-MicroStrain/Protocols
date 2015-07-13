# Wireless Node Commands

**List of Commands:**

* [Short Ping](#short-ping)
* [Long Ping](#long-ping)
* [Read EEPROM](#read-node-eeprom)
* [Write EEPROM](#write-node-eeprom)
* [Initiate Sleep Mode](#initiate-sleep-mode)
* [Set to Idle](#set-to-idle)
* [Arm for Datalogging](#arm-node-for-datalogging)
* [Trigger Armed Datalogging](#trigger-armed-datalogging)
* [Page Download](#page-download)
* [Erase Logged Data](#erase-logged-data)
* [Initiate Real-Time Streaming](#initiate-real-time-streaming-legacy)
* [Initiate Low Duty Cycle](#initiate-low-duty-cycle)
* [Initiate Synchronized Sampling](#initiate-synchronized-sampling)
* [Read Single Sensor](#read-single-sensor)
* [Auto-Balance Channel](#auto-balance-channel)

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
uint8_t commandId 	= 0x05;		//Command ID
uint16_t nodeAddress;			//Node Address
uint16_t pageIndex;				//Index of Page to download
```

##### Success Response:
```cpp
uint8_t commandId 	= 0x05;		//Command ID Echo
uint8_t data[264];				//The Page Data (132 2-byte values)
uint16_t checksum;				//Checksum of [data]
```

##### Failure Response:
```cpp
uint8_t commandId 	= 0x05;		//Command ID Echo
uint16_t failId 	= 0x21;		//Fail Indicator
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
uint16_t startOfHeader 			= 0xAAAA;	//Start of Header
uint8_t headerId 				= 0xFD;		//Header ID
uint8_t triggerId;							//Trigger ID
uint8_t headerVerMajor 			= 0x01;		//Header Version (Major)
uint8_t headerVerMinor 			= 0x00;		//Header Version (Minor)
uint16_t numBytesBeforeChInfo;				//# of Bytes before the Channel Info
uint16_t samplesPerDataSet;					//Samples per Data Set
uint16_t sessionIndex;						//Session Index
uint8_t channelMask;						//Active Channel Mask
uint16_t sampleRate;						//Sample Rate
uint16_t numUserBytes;						//# of User Entered Bytes
int8_t userBytes[0-50];						//up to 50 user entered bytes (if any)
uint16_t numBytesPerCh 			= 0x000A;	//# of Bytes per Channel
uint8_t chEquation;							//Channel Info: Equation ID (per channel)
uint8_t chUnit;								//Channel Info: Unit ID (per channel)
float chSlope;								//Channel Info: Slope (per channel)
float chOffset;								//Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd 		= 0x0008;	//# of Bytes before end of header
uint32_t timestampSec;						//UTC Timestamp (Seconds)
uint32_t timestampNano;						//UTC Timestamp (Nanoseconds)
```

##### Header Format Version **2.0**:
```cpp
uint16_t startOfHeader 			= 0xAAAA;	//Start of Header
uint8_t headerId 				= 0xFD;		//Header ID
uint8_t triggerId;							//Trigger ID
uint8_t headerVerMajor 			= 0x02;		//NEW: Header Version (Major)
uint8_t headerVerMinor 			= 0x00;		//NEW: Header Version (Minor)
uint16_t numBytesBeforeChInfo;				//# of Bytes before the Channel Info
uint16_t samplesPerDataSet;					//Samples per Data Set
uint16_t sessionIndex;						//Session Index
uint8_t channelMask;						//Active Channel Mask
uint16_t sampleRate;						//Sample Rate
uint8_t dataType;							//NEW: Data Type
uint8_t reserved;							//NEW: RESERVED
uint16_t numUserBytes;						//# of User Entered Bytes
int8_t userBytes[0-50];						//up to 50 user entered bytes (if any)
uint16_t numBytesPerCh 			= 0x000A;	//# of Bytes per Channel
uint8_t chEquation;							//Channel Info: Equation ID (per channel)
uint8_t chUnit;								//Channel Info: Unit ID (per channel)
float chSlope;								//Channel Info: Slope (per channel)
float chOffset;								//Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd 		= 0x0008;	//# of Bytes before end of header
uint32_t timestampSec;						//UTC Timestamp (Seconds)
uint32_t timestampNano;						//UTC Timestamp (Nanoseconds)
```

##### Header Format Version **2.1**:
```cpp
uint16_t startOfHeader 			= 0xAAAA;	//Start of Header
uint8_t headerId 				= 0xFD;		//Header ID
uint8_t triggerId;							//Trigger ID
uint8_t headerVerMajor 			= 0x02;		//NEW: Header Version (Major)
uint8_t headerVerMinor 			= 0x01;		//NEW: Header Version (Minor)
uint16_t numBytesBeforeChInfo;				//# of Bytes before the Channel Info
uint16_t samplesPerDataSet;					//NEW: Samples per Data Set / 100
uint16_t sessionIndex;						//Session Index
uint8_t channelMask;						//Active Channel Mask
uint16_t sampleRate;						//Sample Rate
uint8_t dataType;							//Data Type
uint8_t reserved;							//RESERVED
uint16_t numUserBytes;						//# of User Entered Bytes
int8_t userBytes[0-50];						//up to 50 user entered bytes (if any)
uint16_t numBytesPerCh 			= 0x000A;	//# of Bytes per Channel
uint8_t chEquation;							//Channel Info: Equation ID (per channel)
uint8_t chUnit;								//Channel Info: Unit ID (per channel)
float chSlope;								//Channel Info: Slope (per channel)
float chOffset;								//Channel Info: Offset (per channel)
//Repeat of Channel Info bytes for each Active Channel in channelMask
uint16_t numBytesBeforeEnd 		= 0x0008;	//# of Bytes before end of header
uint32_t timestampSec;						//UTC Timestamp (Seconds)
uint32_t timestampNano;						//UTC Timestamp (Nanoseconds)
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
2 		|float    | floating point value with any conversions (slope & offset) applied

**User Entered Bytes:** Up to 50 optional user entered bytes may have been sent to the node when triggering an Armed Datalogging session. The *numUserBytes* byte specifies how many user bytes follow in the packet. If the number of user entered bytes is an odd number, there will be 1 extra “buffer” byte appended
to the user data that should be discarded.

**Channel Information:** The Channel Information bytes show which calibration coefficients were enabled during datalogging for each of the active channels.

**Timestamp:** The UTC timestamp represents the starting time of the logged session (the time applied to the very first data point). The nanoseconds should be appended to the seconds of the given timestamp. By incrementing the initial UTC timestamp by the sample rate, you can determine the exact time of each stored data point.

**Session Data:** During the actual datalogging session, the data from each active channel on the Node is written consecutively to the memory pages. For example, a Node with 3 active channels (CH1, CH3, CH4) would write data as CH1, CH3, CH4; CH1, CH3, CH4 and so forth. This data comes off the Node in the same
pattern during download. These byte immediately follow the header bytes.

<br>
## Erase Logged Data

The **Erase Logged Data** command is used to erase all sampled data stored on the Node's memory. This cannot be undone.

##### Command:
```cpp
uint8_t commandId 		= 0x06;			//Command ID
uint16_t nodeAddress;					//Node Address
uint32_t commandBytes 	= 0x08100CFF;	//Command Bytes
```

##### Success Response:
```cpp
uint8_t commandId 		= 0x06;			//Command ID Echo
```

##### Failure Response:
```cpp
uint8_t failId 			= 0x21;			//Fail Indicator
```

##### Notes:
**Response:** The response is returned immediately when the erasing processes begins, and no acknowledgment is sent when the process completes. The process may take up to 5 seconds, and the Node will not respond to any commands until the erasing is complete. Completion of the erase can be detected by repeatedly pinging the Node; when the erase is complete, the Node will return to idle mode and respond successfully to the ping.

<br>
## Initiate Real-Time Streaming (Legacy)

The **Initiate Real-Time Streaming** command is used to start a real-time streaming session on a Node. The Node will respond by immediately sending a stream of data packets as the sensors are read. 

**Note:** The Real-Time Streaming sampling mode is a legacy sampling mode and is no longer a recommended method of sampling. The sample rate is not consistent, data is not timestamped, you can only sample 1 Node at a time, and the data packet provides very little information.

##### Command:
```cpp
uint8_t commandId 		= 0x38;		//Command ID
uint16_t nodeAddress;				//Node Address
```

##### Response:
Parsing of the streaming packets should begin with the first 0xFF byte. The 0xFF byte is the header of the first valid data packet shown below as Byte 1. Each successive 0xFF indicates the start of a new data packet and the end of the previous packet.

Response Data Packet:
```cpp
uint8_t commandId 		= 0xFF;		//Command ID Echo
uint16_t channelValue;				//Channel Value for 1st active channel
//Repeat channelValue bytes for each active channel
uint8_t checksum;					//Checksum for [channelValue] bytes
```

##### Notes:
**Terminating Streaming:** Streaming may be stopped at any time by issuing any byte to the Base Station. This will cause the Base Station to stop streaming. It will not however cause the Node to stop streaming. The Node will continue to stream until the set (finite) duration has elapsed, the power on the Node is cycled,
or the Set to Idle command has been issued to the Node.

**End of Stream:** The normal end of a finite stream is marked by 4-6 consecutive 0xAA (170) bytes. When parsing the stream, these bytes should be used as a signal that finite streaming has ended.

<br>
## Initiate Low Duty Cycle

The **Initiate Low Duty Cycle (LDC)** command is used to put the Node in LDC sampling mode.

The Low Duty Cycle sampling mode is a non-synchronized, low-latency form of sampling. While multiple Nodes can be started sampling, they are not part of a synchronized network. This can cause data packets to be sent over the air at the same time, resulting in data loss. If low-latency is not a requirement, it is highly recommended that you use the [Synchronized Sampling Mode](initiate-synchronized-sampling).

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x05;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t commandId 		= 0x0038;	//Command ID
uint16_t checksum;					//Checksum of [stopFlag - commandId]
```

##### Initial Response:
An initial response comes directly from the Base Station to acknowledge that the command was received by the Base Station and sent to the Node.
```cpp
uint8_t packetSentAck 	= 0xAA;		//Package Sent Acknowledgement
```

##### Success Response:
No Response.

##### Failure Response:
No Response.

<br>
## Initiate Synchronized Sampling

The **Initiate Synchronized Sampling command** is used to put the Node into Synchronized Sampling mode. Once in this mode, the node must receive a beacon from the Base Station to begin sampling and transmitting data packets.

For Synchronized Sampling mode, the wireless sensor network needs to be configured so that each node is assigned an appropriate TDMA slot prior to issuing the Initiate Synchronized Sampling command. To set up the wireless sensor network, use either the Synchronized Sampling Network within the MicroStrain provided desktop software, or the MicroStrain Communication Library (MSCL). Failure to configure the network correctly will lead to wireless packets colliding, resulting in data loss.

##### Command:
```cpp
uint8_t startByte 		= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 		= 0x05;		//Delivery Stop Flag
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x02;		//Payload Length
uint16_t commandId 		= 0x003B;	//Command ID
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
uint8_t appDataType 	= 0x00;		//App Data Type
uint16_t nodeAddress;				//Node Address
uint8_t payloadLen 		= 0x03;		//Payload Length
uint16_t commandId		= 0x003B;	//Command ID Echo
uint8_t notUsed			= 0x00;		//RESERVED
int8_t nodeRssi;					//Node RSSI
int8_t baseRssi;					//Base RSSI
uint16_t checksum;					//Checksum of [stopFlag - notUsed]
```

##### Failure Response:
No Response.

<br>
## Read Single Sensor

The **Read Single Sensor** command is used to read the current value of a single channel on the Node.

##### Command:
```cpp
uint8_t commandId 		= 0x03;		//Command ID
uint16_t nodeAddress;				//Node Address
uint8_t commandByte 	= 0x01;		//Command Byte
uint8_t channelNumber;				//Channel Number
```

##### Success Response:
```cpp
uint8_t commandId 		= 0x03;		//Command ID Echo
uint16_t channelValue;				//Value of the Requested Channel
uint16_t checksum;					//Checksum of [channelValue]
```

##### Failure Response:
```cpp
uint8_t failId 			= 0x21;		//Failure Indicator
```

##### Notes:
**Erroneous Data:** Values read using the Read Single Sensor command may be off due to there being no excitation time taken into account. The other full sampling modes use a Sampling Delay, which is an amount of time between sensor excitation power up and A/D sampling.

<br>
## Auto-Balance Channel

The **Auto-Balance Channel** command is used to auto-balance a particular channel on the Node. This command is only applicable to the differential channels on certain Nodes.

##### Command:
```cpp
uint8_t commandId 		= 0x62;		//Command ID
uint16_t nodeAddress;				//Node Address
uint8_t channelNumber;				//Channel # to Balance
uint16_t targetValue;				//Target Balance Value
```

##### Success Response:
No Response.

##### Failure Response:
No Response.

##### Notes:
**Target Balance Value:** The target balance value represents the desired sensor output value in bits. All differential inputs have a programmable offset feature that allows the user to trim sensor offset (see hardware user manual for more information). This programmable offset can be manually altered via Node EEPROM, or auto-tuned such that the sensor output is balanced to a user-defined target. For example, a common use is to auto-balance to mid-scale (2048 bits) to obtain maximum bipolar dynamic range.
