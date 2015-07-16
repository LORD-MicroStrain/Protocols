# Wireless Data Packets

**List of Packets:**

* [Low Duty Cycle (LDC) Packet](#low-duty-cycle-ldc-packet)
* [Buffered Low Duty Cycle Packet](#buffered-low-duty-cycle-packet)
* [Synchronized Sampling Packet](#synchronized-sampling-packet)
* [Asynchronous Digital-Only Packet](#asynchronous-digital-only-packet)
* [Asynchronous Digital & Analog Packet](#asynchronous-digital--analog-packet)
* [Diagnostic Packet](#diagnostic-packet)

## Low Duty Cycle (LDC) Packet

```cpp
uint8_t startByte 					= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 					= 0x07;		//Delivery Stop Flag
uint8_t appDataType 				= 0x04;		//App Data Type
uint16_t nodeAddress;							//Node Address
uint8_t payloadLen;								//Payload Length
uint8_t appId 						= 0x02;		//App ID
uint8_t channelMask;							//Active Channel Mask
uint8_t sampleRate;								//Sample Rate
uint8_t dataType;								//Data Type
uint16_t tick;									//Timer Tick
uint16_t | uint32_t | float chData;				//Channel Data (per channel)
//Repeat Channel Data bytes for each active channel
int8_t reserved;								//RESERVED
int8_t baseRssi;								//Base Station RSSI
uint16_t checksum;								//Checksum of [stopFlag - chData]
```

## Buffered Low Duty Cycle Packet
```cpp
uint8_t startByte 					= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 					= 0x07;		//Delivery Stop Flag
uint8_t appDataType 				= 0x0D;		//App Data Type
uint16_t nodeAddress;							//Node Address
uint8_t payloadLen;								//Payload Length
uint8_t appId 						= 0x02;		//App ID
uint8_t channelMask;							//Active Channel Mask
uint8_t sampleRate;								//Sample Rate
uint8_t dataType;								//Data Type
uint16_t tick;									//Sweep Tick
uint16_t | uint32_t | float chData;				//Channel Data (per channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;								//Node RSSI
int8_t baseRssi;								//Base Station RSSI
uint16_t checksum;								//Checksum of [stopFlag - chData]
```

## Synchronized Sampling Packet
```cpp
uint8_t startByte 					= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 					= 0x07;		//Delivery Stop Flag
uint8_t appDataType 				= 0x0A;		//App Data Type
uint16_t nodeAddress;							//Node Address
uint8_t payloadLen;								//Payload Length
uint8_t sampleMode;								//Sample Mode
uint8_t channelMask;							//Active Channel Mask
uint8_t sampleRate;								//Sample Rate
uint8_t dataType;								//Data Type
uint16_t tick;									//Sweep Tick
uint32_t timestampSec;							//UTC Timestamp (seconds)
uint32_t timestampNano;							//UTC Timestamp (nanoseconds)
uint16_t | uint32_t | float chData;				//Channel Data (per channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;								//Node RSSI
int8_t baseRssi;								//Base Station RSSI
uint16_t checksum;								//Checksum of [stopFlag - chData]
```

#####Notes:
**Sample Mode:**

 * 0x01 - Burst Mode
 * 0x02 - Continuous Mode

**Timestamp / Tick:**
Although each packet may contain more than one sweep per channel, there is only one timestamp and tick acquired per packet. Therefore the tick and timestamp values must be incremented manually for each sweep in the packet. This can be done via the following:

* Using the sample rate of the node, determine your increment value:
  * If sample rate is 32 Hz, the increment is 0.03125. (1 / 32)
  * If sample rate is 1 per 2 seconds, the increment is 2.
  * Multiply the increment by 1,000,000,000 to convert to nanoseconds.
* For each sweep in the packet, add the calculated value to the original timestamp.
* For each sweep, increment the tick by 1.

**Channel Data:**
Multiple sweeps of data per channel may be contained in one packet. The number of sweeps in the packet can be determined via the following:

* bytesBeforeData = 14
* bytesPerSample = 2 for uint16 or 4 for uint32 or float data.
* numSweeps = ((payloadLen – bytesBeforeData) / numActiveChannels) / bytesPerSample)

Channel data should be parsed in the following manner:

- Sweep 1, First active channel
- Sweep 1, Next active channel (Repeat for each active channel)
- Sweep 2, First active channel
- Sweep 2, Next active channel (Repeat for each active channel)
- Repeat for each Sweep in the packet 

## Asynchronous Digital-Only Packet
The Asynchronous Digital-Only data packet contains time and digital state values collected when a Node was triggered by digital pulses.

```cpp
uint8_t startByte 					= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 					= 0x07;		//Delivery Stop Flag
uint8_t appDataType 				= 0x0E;		//App Data Type
uint16_t nodeAddress;							//Node Address
uint8_t payloadLen;								//Payload Length
uint16_t channelMask;							//Digital Channel Mask
uint16_t tick;									//Event Tick
uint32_t timestampSec;							//UTC Timestamp (seconds)
uint32_t timestampNano;							//UTC Timestamp (nanoseconds)
uint16_t timestampOffset_Evt1;					//Timestamp Offset - Event 1
uint16_t digitalChannelData_Evt1;					//Digital Channel Data - Event 1
//Repeat Timestamp and Digital Channel bytes for all Events
int8_t nodeRssi;								//Node RSSI
int8_t baseRssi;								//Base Station RSSI
uint16_t checksum;								//Checksum of [stopFlag - digitalChannelData_EvtX]
```

#####Notes:
**Digital Channel Mask:** The Digital Channel Mask represents the digital channels that are actively being monitored by the Node.

**Event Tick:** The Event Tick represents a counter for each event. Although multiple events may be in the same packet, only one Event Tick will be found per packet. The tick for each event can be found by incrementing the Event Tick for each event that is contained in that packet.

**Timestamp:** The UTC Timestamp bytes represent the initial timestamp in which each Event’s Timestamp Offset must be added to in order to calculate the UTC Timestamp for each Event.

**Events:** Each event contained in the packet is made up of a 2-byte Timestamp Offset and 2 bytes of Digital Channel Data. The Timestamp Offset must be divided by 32,768 to get its time in seconds. Each bit in the digital channel data represents a digital line. However, the Digital Channel Mask should be interrogated to determine which of these lines have a valid value. Multiple events may be contained in one packet. The number of events in the packet can be determined via the following: 

    #Events = ((Payload Length - 12) / 4)

Each event has a timestamp offset that much be added to the packet’s absolute timestamp. This can be done via the following:

    EventTimestamp = PacketTimestamp + (EventTimestampOffset / 32,768)

## Asynchronous Digital & Analog Packet
The Asynchronous Digital & Analog data packet contains time, digital state, and analog sensor values collected when a Node was triggered by digital pulses.

```cpp
uint8_t startByte 					= 0xAA;			//Start of Packet Byte
uint8_t stopFlag 					= 0x07;			//Delivery Stop Flag
uint8_t appDataType 				= 0x0F;			//App Data Type
uint16_t nodeAddress;								//Node Address
uint8_t payloadLen;									//Payload Length
uint16_t channelMask;								//Channel Mask
uint8_t dataType;									//Data Type
uint16_t tick;										//Event Tick
uint32_t timestampSec;								//UTC Timestamp (seconds)
uint32_t timestampNano;								//UTC Timestamp (nanoseconds)
uint16_t timestampOffset_Evt1;						//Timestamp Offset - Event 1
uint16_t digitalChannelData_Evt1;					//Digital Channel Data - Event 1
uint16_t | uint32_t | float	analogChannelData_Evt1;	//Analog Channel Data - Event 1
//Repeat Analog Channel Data for each digital channel that is active (high) in the Digital Channel Data bytes for the current Event.
//Repeat Timestamp and Digital Channel Data, and Analog Channel Data bytes for all Events
int8_t nodeRssi;									//Node RSSI
int8_t baseRssi;									//Base Station RSSI
uint16_t checksum;									//Checksum of [stopFlag - analogChannelData_EvtX]
```

#####Notes:
**Digital Channel Mask:** The Digital Channel Mask represents the digital channels that are actively being monitored by the Node.

**Data Type:** The Data Type determines the format of **Analog** data that is transmitted in the packet.

**Event Tick:** The Event Tick represents a counter for each event. Although multiple events may be in the same packet, only one Event Tick will be found per packet. The tick for each event can be found by incrementing the Event Tick for each event that is contained in that packet.

**Timestamp:** The UTC Timestamp bytes represent the initial timestamp in which each Event’s Timestamp Offset must be added to in order to calculate the UTC Timestamp for each Event.

**Events:** Each event contained in the packet is made up of a 2-byte timestamp offset, 2-bytes of digital channel data, and X bytes of analog channel data. The Timestamp Offset must be divided by 32,768 to get its time in seconds. Each bit in the digital channel data represents a digital line. However, the Channel Mask should be interrogated to determine which of these lines have a valid value. The analog channel data will only be present when the digital channel line is active (a value of 1). Note that the analog channel data needs to be read off in the specific data type that is denoted by the Data Type byte.

*Example: *  The first event in the packet contains a digital value of 13, which is 0000 0000 0000 1101 in binary, meaning digital lines 1, 3, and 4 are active. The Data Type of the packet is 0x02, meaning the analog data points are 4-byte floating point values. So the next 12 bytes (3 channels * 4 bytes per ch) in the packet will be the analog values for channels 1, 3, and 4.

Each packet may contain more than one event. Each event has a timestamp offset that much be added to the packet’s absolute timestamp. This can be done via the following:

    EventTimestamp = PacketTimestamp + (EventTimestampOffset / 32,768)

## Diagnostic Packet
```cpp
uint8_t startByte 					= 0xAA;		//Start of Packet Byte
uint8_t stopFlag 					= 0x07;		//Delivery Stop Flag
uint8_t appDataType 				= 0x11;		//App Data Type
uint16_t nodeAddress;							//Node Address
uint8_t payloadLen;								//Payload Length
uint8_t packetInterval;							//Packet Interval
uint16_t tick;									//Tick
uint8_t info1Len;								//Info Item 1 Length
uint8_t info1Id;								//Info Item 1 ID
uint8_t | uint16_t | uint32_t info1Val;			//Info Item 1 Value
//Repeat Info Item Length, ID, and Value for all the Info Items in the packet
int8_t nodeRssi;								//Node RSSI
int8_t baseRssi;								//Base Station RSSI
uint16_t checksum;								//Checksum of [stopFlag - infoXVal]
```

#####Notes:
**Diagnostic Packet Interval:**
The interval of which the Diagnostic Packet is transmitted. The 2 most significant bits of this byte signify the interval type (seconds, minutes, or hours). The remaining 6 bits are the interval value. The interval types are as follows (shows in binary):

* 00 = Seconds
* 01 = Minutes
* 10 = Hours

Example (in binary):
0110 1011 = 43 minutes  -> *first 01 represents minutes, 10 1011 represents the value 43.*

**Tick:**
The Tick represents a counter for the Diagnostic Packet, signifying how many of these packets have been sent. When this value reaches the max 2-byte value (0xFFFF), it will roll over to 0.

**Info Items:**
An Info Item consists of Length, ID, and Value bytes. Each Info Item can be parsed by first looking at the length byte to determine how many bytes make up the rest of the rest of the Info Item (ID and Value). The Info Item ID can then be compared against the table below to determine how to parse the value bytes that follow. Multiple Info Items can be in one packet. Use the payload length to determine the number of Info Items in the packet.

**Info Item Length:**
The length (# of bytes) of the Info Item, including the Info Item ID and Info Item Value bytes. This length
value does not include the Info Item Length byte itself. 

**Info Item ID / Value:**
The Info Item ID represents the type of information that is given in the next Info Item Value bytes. The following are the supported IDs:

ID  | Description   | Data Values | # Bytes | Type | Unit 
----|---------------|----------------|----------|-------|------
0x01| Transmit Info | Total Transmissions <br> Total Retransmissions <br> Total Dropped Packets | 4 <br> 4 <br> 2 | uint32 <br> uint32 <br> uint16  | counts <br> counts <br> counts
0x02 | Active Running Time | - | 4 | uint32 | seconds
0x03 | Battery Life Remaining | - | 1 | uint8 | percent


* **(0x01) Transmit Info**
	* **Total Transmissions** - # of unique packets transmitted (not including retransmissions)
	* **Total Retransmissions** - # of retransmitted packets (packets are retransmitted when a node doesn't receive an acknowledgment from the base station)
	* **Total Dropped Packets** - # of packets node has discarded due to buffer overflow or exceeding the max # of retransmissions per packet
* **(0x02) Active Running Time** - # of seconds the node has been in a sampling mode
* **(0x03) Battery Life Remaining** - % estimated battery level

*Full Example:*
If the Info Item Length byte is 0x0B, the next 11 bytes make up the Info Item ID and Value. If the next byte is 0x01, then we know the Info Item Value is signifying Transmit Info which is made up of Total Transmissions, Total Retransmissions, and Total Dropped Packets. From the table we know to parse the next 4 bytes as a uint32 representing the Total Transmissions, the next 4 bytes as a uint32 representing the Total Retransmissions, and the last 2 bytes as a uint16 representing the Total Dropped Packets.
