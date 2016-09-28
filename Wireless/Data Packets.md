# Wireless Data Packets

**List of Packets:**

Packet      | App Data Type
-------------|--------------
[Low Duty Cycle Packet (v1)](#low-duty-cycle-ldc-packet-v1) | 0x04
[Low Duty Cycle Packet (v2)](#low-duty-cycle-ldc-packet-v2) | 0x14
[Buffered Low Duty Cycle Packet (v1)](#buffered-low-duty-cycle-packet-v1) | 0x0D
[Buffered Low Duty Cycle Packet (v2)](#buffered-low-duty-cycle-packet-v2) | 0x1D
[Synchronized Sampling Packet (v1)](#synchronized-sampling-packet-v1) | 0x0A
[Synchronized Sampling Packet (v2)](#synchronized-sampling-packet-v2) | 0x1A
[Asynchronous Digital-Only Packet](#asynchronous-digital-only-packet) | 0x0E
[Asynchronous Digital & Analog Packet](#asynchronous-digital--analog-packet) | 0x0F
[Structural Health Packet (v1)](#structural-health-packet-v1) | 0xA0
[Structural Health Packet (v2)](#structural-health-packet-v2) | 0xA0
[Raw Angle Strain Packet (Specific Angle Mode)](#raw-angle-strain-packet-specific-angle-mode) | 0xA3
[Raw Angle Strain Packet (Distributed Angle Mode)](#raw-angle-strain-packet-distributed-angle-mode) | 0xA3
[Diagnostic Packet](#diagnostic-packet) | 0x11
[Node Discovery Packet (v1)](#node-discovery-packet-v1) | 0x00
[Node Discovery Packet (v2)](#node-discovery-packet-v2) | 0x17
[Node Discovery Packet (v3)](#node-discovery-packet-v3) | 0x18
[Node Discovery Packet (v4)](#node-discovery-packet-v4) | 0x16
[Beacon Echo Packet](#beacon-echo-packet) | 0x10
[RF Sweep Packet](#rf-sweep-packet) | 0x31

## Low Duty Cycle (LDC) Packet (v1)

```cpp
uint8_t startByte                 = 0xAA; //Start of Packet Byte
uint8_t stopFlag                  = 0x07; //Delivery Stop Flag
uint8_t appDataType               = 0x04; //App Data Type
uint16_t nodeAddress;                     //Node Address
uint8_t payloadLen;                       //Payload Length
uint8_t appId                     = 0x02; //App ID
uint8_t channelMask;                      //Active Channel Mask
uint8_t sampleRate;                       //Sample Rate
uint8_t dataType;                         //Data Type
uint16_t tick;                            //Timer Tick
uint16_t | uint32_t | float chData[N];     //Channel Data (per active channel)
//Repeat Channel Data bytes for each active channel
int8_t reserved;                          //RESERVED
int8_t baseRssi;                          //Base Station RSSI
uint16_t checksum;                        //Checksum of [stopFlag - chData]
```

## Low Duty Cycle (LDC) Packet (v2)

Version 2 of the Low Duty Cycle Packet supports up to 16 channels (versus 8 in v1).

```cpp
uint8_t startByte                 = 0xAA; //Start of Packet Byte
uint8_t stopFlag                  = 0x07; //Delivery Stop Flag
uint8_t appDataType               = 0x14; //App Data Type
uint16_t nodeAddress;                     //Node Address
uint8_t payloadLen;                       //Payload Length
uint16_t channelMask;                     //Active Channel Mask
uint8_t sampleRate;                       //Sample Rate
uint8_t appIdAndDataType          = 0x02; //App ID / Data Type
uint16_t tick;                            //Timer Tick
uint16_t | uint32_t | float chData[];     //Channel Data (per active channel)
//Repeat Channel Data bytes for each active channel
int8_t reserved;                          //RESERVED
int8_t baseRssi;                          //Base Station RSSI
uint16_t checksum;                        //Checksum of [stopFlag - chData]
```

#####Notes:

**Data Type:**

The `appIdAndDataType` byte uses the last 4 (Least Significant) bits as the Data Type:
 * 0x01 = 2 byte unsigned integer (uint16) (bit-shifted)
 * 0x02 = 4 byte float (float)
 * 0x03 = 2 byte unsigned integer (uint16)
 * 0x04 = 4 byte unsigned integer (uint32)

## Buffered Low Duty Cycle Packet (v1)
```cpp
uint8_t startByte                   = 0xAA; //Start of Packet Byte
uint8_t stopFlag                    = 0x07; //Delivery Stop Flag
uint8_t appDataType                 = 0x0D; //App Data Type
uint16_t nodeAddress;                       //Node Address
uint8_t payloadLen;                         //Payload Length
uint8_t appId                       = 0x02; //App ID
uint8_t channelMask;                        //Active Channel Mask
uint8_t sampleRate;                         //Sample Rate
uint8_t dataType;                           //Data Type
uint16_t tick;                              //Sweep Tick
uint16_t | uint32_t | float chData[];       //Channel Data (per active channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;                            //Node RSSI
int8_t baseRssi;                            //Base Station RSSI
uint16_t checksum;                          //Checksum of [stopFlag - chData]
```

## Buffered Low Duty Cycle Packet (v2)

Version 2 of the Buffered Low Duty Cycle Packet supports up to 16 channels (versus 8 in v1).

```cpp
uint8_t startByte                   = 0xAA; //Start of Packet Byte
uint8_t stopFlag                    = 0x07; //Delivery Stop Flag
uint8_t appDataType                 = 0x1D; //App Data Type
uint16_t nodeAddress;                       //Node Address
uint8_t payloadLen;                         //Payload Length
uint16_t channelMask;                       //Active Channel Mask
uint8_t sampleRate;                         //Sample Rate
uint8_t appIdAndDataType;                   //App ID / Data Type
uint16_t tick;                              //Sweep Tick
uint16_t | uint32_t | float chData[];       //Channel Data (per channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;                            //Node RSSI
int8_t baseRssi;                            //Base Station RSSI
uint16_t checksum;                          //Checksum of [stopFlag - chData]
```

#####Notes:

**Data Type:**

The `appIdAndDataType` byte uses the last 4 (Least Significant) bits as the Data Type:
 * 0x01 = 2 byte unsigned integer (uint16) (bit-shifted)
 * 0x02 = 4 byte float (float)
 * 0x03 = 2 byte unsigned integer (uint16)
 * 0x04 = 4 byte unsigned integer (uint32)

## Synchronized Sampling Packet (v1)
```cpp
uint8_t startByte                   = 0xAA; //Start of Packet Byte
uint8_t stopFlag                    = 0x07; //Delivery Stop Flag
uint8_t appDataType                 = 0x0A; //App Data Type
uint16_t nodeAddress;                       //Node Address
uint8_t payloadLen;                         //Payload Length
uint8_t sampleMode;                         //Sample Mode
uint8_t channelMask;                        //Active Channel Mask
uint8_t sampleRate;                         //Sample Rate
uint8_t dataType;                           //Data Type
uint16_t tick;                              //Sweep Tick
uint32_t timestampSec;                      //UTC Timestamp (seconds)
uint32_t timestampNano;                     //UTC Timestamp (nanoseconds)
uint16_t | uint32_t | float chData[];       //Channel Data (per active channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;                            //Node RSSI
int8_t baseRssi;                            //Base Station RSSI
uint16_t checksum;                          //Checksum of [stopFlag - chData]
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


## Synchronized Sampling Packet (v2)

Version 2 of the Synchronized Sampling Packet supports up to 16 channels (versus 8 in v1).

```cpp
uint8_t startByte               = 0xAA;   //Start of Packet Byte
uint8_t stopFlag                = 0x07;   //Delivery Stop Flag
uint8_t appDataType             = 0x1A;   //App Data Type
uint16_t nodeAddress;                     //Node Address
uint8_t payloadLen;                       //Payload Length
uint16_t channelMask;                     //Active Channel Mask
uint8_t sampleRate;                       //Sample Rate
uint8_t sampleModeAndDataType;            //Sample Mode / Data Type
uint16_t tick;                            //Sweep Tick
uint32_t timestampSec;                    //UTC Timestamp (seconds)
uint32_t timestampNano;                   //UTC Timestamp (nanoseconds)
uint16_t | uint32_t | float chData[];     //Channel Data (per active channel, per sweep)
//Repeat Channel Data bytes for each active channel, and for each sweep
int8_t nodeRssi;                          //Node RSSI
int8_t baseRssi;                          //Base Station RSSI
uint16_t checksum;                        //Checksum of [stopFlag - chData]
```

#####Notes:
**Sample Mode:**

The `sampleModeAndDataType` byte uses the first 4 (Most Significant) bits as the Sample Mode:

 * 0x01 - Burst Mode
 * 0x02 - Continuous Mode

**Sample Mode:**

The `sampleModeAndDataType` byte uses the last 4 (Least Significant) bits as the Data Type:
 * 0x01 = 2 byte unsigned integer (uint16) (bit-shifted)
 * 0x02 = 4 byte float (float)
 * 0x03 = 2 byte unsigned integer (uint16)
 * 0x04 = 4 byte unsigned integer (uint32)

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
uint8_t startByte           = 0xAA;        //Start of Packet Byte
uint8_t stopFlag            = 0x07;        //Delivery Stop Flag
uint8_t appDataType         = 0x0E;        //App Data Type
uint16_t nodeAddress;                      //Node Address
uint8_t payloadLen;                        //Payload Length
uint16_t channelMask;                      //Digital Channel Mask
uint16_t tick;                             //Event Tick
uint32_t timestampSec;                     //UTC Timestamp (seconds)
uint32_t timestampNano;                    //UTC Timestamp (nanoseconds)
uint16_t timestampOffset_Evt1;             //Timestamp Offset - Event 1
uint16_t digitalChannelData_Evt1;          //Digital Channel Data - Event 1
//Repeat Timestamp and Digital Channel bytes for all Events
int8_t nodeRssi;                           //Node RSSI
int8_t baseRssi;                           //Base Station RSSI
uint16_t checksum;                         //Checksum of [stopFlag - digitalChannelData_EvtX]
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
uint8_t startByte           = 0xAA;                  //Start of Packet Byte
uint8_t stopFlag            = 0x07;                  //Delivery Stop Flag
uint8_t appDataType         = 0x0F;                  //App Data Type
uint16_t nodeAddress;                                //Node Address
uint8_t payloadLen;                                  //Payload Length
uint16_t channelMask;                                //Channel Mask
uint8_t dataType;                                    //Data Type
uint16_t tick;                                       //Event Tick
uint32_t timestampSec;                               //UTC Timestamp (seconds)
uint32_t timestampNano;                              //UTC Timestamp (nanoseconds)
uint16_t timestampOffset_Evt1;                       //Timestamp Offset - Event 1
uint16_t digitalChannelData_Evt1;                    //Digital Channel Data - Event 1
uint16_t | uint32_t | float  analogChannelData_Evt1; //Analog Channel Data - Event 1
//Repeat Analog Channel Data for each digital channel that is active (high) in the Digital Channel Data bytes for the current Event.
//Repeat Timestamp and Digital Channel Data, and Analog Channel Data bytes for all Events
int8_t nodeRssi;                                     //Node RSSI
int8_t baseRssi;                                     //Base Station RSSI
uint16_t checksum;                                   //Checksum of [stopFlag - analogChannelData_EvtX]
```

#####Notes:
**Digital Channel Mask:** The Digital Channel Mask represents the digital channels that are actively being monitored by the Node.

**Data Type:** The Data Type determines the format of **Analog** data that is transmitted in the packet.

**Event Tick:** The Event Tick represents a counter for each event. Although multiple events may be in the same packet, only one Event Tick will be found per packet. The tick for each event can be found by incrementing the Event Tick for each event that is contained in that packet.

**Timestamp:** The UTC Timestamp bytes represent the initial timestamp in which each Event’s Timestamp Offset must be added to in order to calculate the UTC Timestamp for each Event.

**Events:** Each event contained in the packet is made up of a 2-byte timestamp offset, 2-bytes of digital channel data, and X bytes of analog channel data. The Timestamp Offset must be divided by 32,768 to get its time in seconds. Each bit in the digital channel data represents a digital line. However, the Channel Mask should be interrogated to determine which of these lines have a valid value. The analog channel data will only be present when the digital channel line is active (a value of 1). Note that the analog channel data needs to be read off in the specific data type that is denoted by the Data Type byte.

*Example:*  The first event in the packet contains a digital value of 13, which is 0000 0000 0000 1101 in binary, meaning digital lines 1, 3, and 4 are active. The Data Type of the packet is 0x02, meaning the analog data points are 4-byte floating point values. So the next 12 bytes (3 channels * 4 bytes per ch) in the packet will be the analog values for channels 1, 3, and 4.

Each packet may contain more than one event. Each event has a timestamp offset that much be added to the packet’s absolute timestamp. This can be done via the following:

    EventTimestamp = PacketTimestamp + (EventTimestampOffset / 32,768)


## Structural Health Packet (v1)
The Structural Health Packet contains structural health data.

```cpp
uint8_t startByte           = 0xAA;                  //Start of Packet Byte
uint8_t stopFlag            = 0x07;                  //Delivery Stop Flag
uint8_t appDataType         = 0xA0;                  //App Data Type
uint16_t nodeAddress;                                //Node Address
uint8_t payloadLen;                                  //Payload Length
uint8_t appId               = 0xA0;                  //App ID
uint8_t angleId;                                     //Angle ID
uint8_t mode;                                        //Mode (0 = normal, 1 = idle)
uint16_t binSize;                                    //Size of each Bin
uint16_t binStart;                                   //The start of bin 1 (in microstrain)
uint16_t dataSetId;                                  //Data Set ID # (each ID is used for 3 sets of binned data)
uint32_t uptime;                                     //Uptime counter
float angle;                                         //Angle (in Radians)
float damage;                                        //Damage percentage (0 = new, 100 = dead)
uint32_t binData[21];                                //Binned data
int8_t reserved;                                     //RESERVED
int8_t baseRssi;                                     //Base Station RSSI
uint16_t checksum;                                   //Checksum of [stopFlag - binData]
```

#####Notes:

**Bins**

This packet always contains 21 bins of Histogram data.

**Sample Rate**

The Histogram data in this packet is calculated from the strain sensors using a 32Hz sample rate. The packet itself is transmitted every 30 seconds.


## Structural Health Packet (v2)
The Structural Health Packet contains structural health data.

```cpp
uint8_t startByte           = 0xAA;                  //Start of Packet Byte
uint8_t stopFlag            = 0x07;                  //Delivery Stop Flag
uint8_t appDataType         = 0xA0;                  //App Data Type
uint16_t nodeAddress;                                //Node Address
uint8_t payloadLen;                                  //Payload Length
uint8_t appId               = 0x00;                  //App ID
uint8_t transmitRate;                                //Transmit Rate of the packet
uint8_t sampleRate;                                  //Sample/Processing Rate of the data
uint32_t persistentTick;                             //Count of Histogram Sweeps
float angle;                                         //Angle (in Degrees)
float damage;                                        //Damage percentage (0 = new, 100 = dead)
uint16_t binStart;                                   //The start of bin 1 (in microstrain)
uint16_t binSize;                                    //Size of each Bin
uint32_t binData[21];                                //Binned data
int8_t nodeRssi;                                     //Node RSSI
int8_t baseRssi;                                     //Base Station RSSI
uint16_t checksum;                                   //Checksum of [stopFlag - binData]
```

#####Notes:

**Bins**

This packet always contains 21 bins of Histogram data.

**Persistent Tick**

The persistent tick is a count of the number of "Histogram Sweeps" that have occurred (groups of Histogram packets). This value is persistent in that it doesn't get reset when the Node cycles power. It will, however, get reset when the Clear Histogram command is performed.



## Raw Angle Strain Packet (Specific Angle Mode)
The Raw Angle Strain Packet (Specific Angle Mode) contains strain data at specific angles.

```cpp
uint8_t startByte           = 0xAA;                  //Start of Packet Byte
uint8_t stopFlag            = 0x07;                  //Delivery Stop Flag
uint8_t appDataType         = 0xA3;                  //App Data Type
uint16_t nodeAddress;                                //Node Address
uint8_t payloadLen;                                  //Payload Length
uint8_t appId               = 0x00;                  //App ID
uint8_t sampleRate;                                  //Sample Rate
uint16_t tick;                                       //Timer Tick
uint8_t numAngles;                                   //Number of Angles
float angle;                                         //Angle (in Degrees)
float angleStrainData;                               //Angle Strain Data
//Repeat angle and angleStrainData for the total number of angles
int8_t reserved;                                     //RESERVED
int8_t baseRssi;                                     //Base Station RSSI
uint16_t checksum;                                   //Checksum of [stopFlag - angleStrainData]
```

## Raw Angle Strain Packet (Distributed Angle Mode)
The Raw Angle Strain Packet (Distributed Angle Mode) contains strain data for a range of angles.

```cpp
uint8_t startByte           = 0xAA;                  //Start of Packet Byte
uint8_t stopFlag            = 0x07;                  //Delivery Stop Flag
uint8_t appDataType         = 0xA3;                  //App Data Type
uint16_t nodeAddress;                                //Node Address
uint8_t payloadLen;                                  //Payload Length
uint8_t appId               = 0x01;                  //App ID
uint8_t sampleRate;                                  //Sample Rate
uint16_t tick;                                       //Timer Tick
float angleLowerBound;                               //The lower bound angle (in Degrees)
float angleUpperBound;                               //The upper bound angle (in Degrees)
uint8_t numAngles;                                   //The number of angles
float angleStrainData[numAngles];                    //Angle Strain Data
//Repeat angleStrainData for the total number of angles
int8_t reserved;                                     //RESERVED
int8_t baseRssi;                                     //Base Station RSSI
uint16_t checksum;                                   //Checksum of [stopFlag - angleStrainData]
```


## Diagnostic Packet
```cpp
uint8_t startByte           = 0xAA;          //Start of Packet Byte
uint8_t stopFlag            = 0x07;          //Delivery Stop Flag
uint8_t appDataType         = 0x11;          //App Data Type
uint16_t nodeAddress;                        //Node Address
uint8_t payloadLen;                          //Payload Length
uint16_t packetInterval;                     //Packet Interval
uint16_t tick;                               //Tick
uint8_t info1Len;                            //Info Item 1 Length
uint8_t info1Id;                             //Info Item 1 ID
uint8_t | uint16_t | uint32_t info1Val;      //Info Item 1 Value
//Repeat Info Item Length, ID, and Value for all the Info Items in the packet
int8_t nodeRssi;                             //Node RSSI
int8_t baseRssi;                             //Base Station RSSI
uint16_t checksum;                           //Checksum of [stopFlag - infoXVal]
```

#####Notes:
**Diagnostic Packet Interval:**
The interval of which the Diagnostic Packet is transmitted, in seconds.

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
0x00 | Current State | 0=Idle, 1=Deep Sleep, 2=Active Run, 3=Inactive Run | 1 | uint8 | -
0x01 | Run Time | Idle <br> Deep Sleep <br> Active Run <br> Inactive Run | 4 <br> 4 <br> 4 <br> 4 | uint32 <br> uint32 <br> uint32 <br> uint32 | seconds <br> seconds <br> seconds <br> seconds
0x02 | Reset Counter | - | 2 | uint16 | counts
0x03 | Low Battery Indicator | 0=good, 1=low, 2=critical | 1 | uint8 | -
0x04 | Sample Info | Sweep index <br> Bad sweep count | 4 <br> 4 | uint32 <br> uint32 | counts <br> counts
0x05 | Transmit Info | Total Transmissions <br> Total Retransmissions <br> Total Dropped Packets | 4 <br> 4 <br> 4 | uint32 <br> uint32 <br> uint32 | counts <br> counts <br> counts
0x06 | Built in Test Result | - | 4 | uint32 | -
0x07 | Event Trigger Index | - | 2 | uint16 | -
0x08 | External Power | 0=Not Connected, 1=External Power Connected | 1 | uint8 | -
0x09 | Internal Temperature | - | 1 | int8 | Celsius

* **(0x00) Current State** - The current state that the device is in when the Diagnostic packet was sent.
* **(0x01) Run Time** - The # of seconds the Node has been in each state.
* **(0x02) Reset Counter** - The # of times the Node has reset.
* **(0x03) Low Battery Indicator** - If 1, a low battery event has been detected since the last diagnostic packet. If 2, a critical battery event has been detected since the last diagnostic packet.
* **(0x04) Sample Info**
  * **Sweep index** - The total # of sweeps (good and bad).
  * **Bad sweep count** - The total # of sweeps that failed.
* **(0x05) Transmit Info**
  * **Total Transmissions** - # of unique packets transmitted (not including retransmissions)
  * **Total Retransmissions** - # of retransmitted packets (packets are retransmitted when a node doesn't receive an acknowledgment from the base station)
  * **Total Dropped Packets** - # of packets node has discarded due to buffer overflow or exceeding the max # of retransmissions per packet
* **(0x06) Built in Test Result** - The result of the Built in Test function.
* **(0x07) Event Trigger Index** - The index of the most recent Event Trigger logged to the Node (when this number changes, a new Event occurred.
* **(0x08) External Power** - Flag indicating if external power is connected or not.
* **(0x09) Internal Temperature** - The internal temperature in degrees Celsius.

*Full Example:*
If the Info Item Length byte is 0x0B, the next 11 bytes make up the Info Item ID and Value. If the next byte is 0x01, then we know the Info Item Value is signifying Transmit Info which is made up of Total Transmissions, Total Retransmissions, and Total Dropped Packets. From the table we know to parse the next 4 bytes as a uint32 representing the Total Transmissions, the next 4 bytes as a uint32 representing the Total Retransmissions, and the last 2 bytes as a uint16 representing the Total Dropped Packets.

## Node Discovery Packet (v1)
On power up, the Node will transmit two identification packets. The packets are sent out on all radio frequencies, allowing any Base Station within range to receive the identification packets, regardless of the Base Station’s current frequency assignment. The Base Station immediately passes these packets to the host serial port.

```cpp
uint8_t startByte           = 0xAA;    //Start of Packet Byte
uint8_t stopFlag;                      //Delivery Stop Flag
uint8_t appDataType         = 0x00;    //App Data Type
uint16_t nodeAddress;                  //Node Address
uint8_t payloadLen          = 0x03;    //Payload Length
uint8_t frequency;                     //Radio Frequency the Node is on
uint16_t model;                        //The (legacy) Model Number of the Node
int8_t reserved;                       //RESERVED
int8_t baseRssi;                       //Base Station RSSI
uint16_t checksum;                     //Checksum of [stopFlag - model]
```

## Node Discovery Packet (v2)
On power up, the Node will transmit two identification packets. The packets are sent out on all radio frequencies, allowing any Base Station within range to receive the identification packets, regardless of the Base Station’s current frequency assignment. The Base Station immediately passes these packets to the host serial port.

```cpp
uint8_t startByte       = 0xAA;    //Start of Packet Byte
uint8_t stopFlag        = 0x07;    //Delivery Stop Flag
uint8_t appDataType     = 0x17;    //App Data Type
uint16_t nodeAddress;              //Node Address
uint8_t payloadLen      = 0x0F;    //Payload Length
uint8_t frequency;                 //Radio Frequency the Node is on
uint16_t panId;                    //The PAN ID the Node is on
uint16_t modelNumber;              //The Model Number of the Node
uint16_t modelOption;              //The Model Option of the Node
uint32_t serial;                   //The Serial Number of the Node
uint16_t firmwareVersion;          //The (legacy) Firmware Version of the Node
uint16_t defaultMode;              //The Default Mode of the Node
int8_t reserved;                   //RESERVED
int8_t baseRssi;                   //Base Station RSSI
uint16_t checksum;                 //Checksum of [stopFlag - model]
```
**modelNumber** - The main model of the Node (ex. 6305 = G-Link).

**modelOption** - The specific option of the model. Combine this with the modelNumber to accurately identify the Node (ex. 6305-2000 = G-Link 2G, 6305-3000 = G-Link 10G).

**firmwareVersion** - The firmware version of the Node. Byte 1 is the Major part, and Byte 2 in the Minor part.

## Node Discovery Packet (v3)
On power up, the Node will transmit two identification packets. The packets are sent out on all radio frequencies, allowing any Base Station within range to receive the identification packets, regardless of the Base Station’s current frequency assignment. The Base Station immediately passes these packets to the host serial port.

```cpp
uint8_t startByte       = 0xAA;    //Start of Packet Byte
uint8_t stopFlag        = 0x07;    //Delivery Stop Flag
uint8_t appDataType     = 0x18;    //App Data Type
uint16_t nodeAddress;              //Node Address
uint8_t payloadLen      = 0x11;    //Payload Length
uint8_t frequency;                 //Radio Frequency the Node is on
uint16_t panId;                    //The PAN ID the Node is on
uint16_t modelNumber;              //The Model Number of the Node
uint16_t modelOption;              //The Model Option of the Node
uint32_t serial;                   //The Serial Number of the Node
uint16_t firmwareVersion1;         //The Firmware Version of the Node (part 1)
uint16_t firmwareVersion2;         //The Firmware Version of the Node (part 2)
uint16_t defaultMode;              //The Default Mode of the Node
int8_t reserved;                   //RESERVED
int8_t baseRssi;                   //Base Station RSSI
uint16_t checksum;                 //Checksum of [stopFlag - model]
```
**modelNumber** - The main model of the Node (ex. 6305 = G-Link).

**modelOption** - The specific option of the model. Combine this with the modelNumber to accurately identify the Node (ex. 6305-2000 = G-Link 2G, 6305-3000 = G-Link 10G).

**firmwareVersion** - The firmware version of the Node. Byte 1 is the Major part, while Bytes 2-4 (as a uint32_t) together represent the Minor part.

## Node Discovery Packet (v4)
On power up, the Node will transmit two identification packets. The packets are sent out on all radio frequencies, allowing any Base Station within range to receive the identification packets, regardless of the Base Station’s current frequency assignment. The Base Station immediately passes these packets to the host serial port.

```cpp
uint8_t startByte       = 0xAA;    //Start of Packet Byte
uint8_t stopFlag        = 0x07;    //Delivery Stop Flag
uint8_t appDataType     = 0x16;    //App Data Type
uint16_t nodeAddress;              //Node Address
uint8_t payloadLen      = 0x15;    //Payload Length
uint8_t frequency;                 //Radio Frequency the Node is on
uint16_t panId;                    //The PAN ID the Node is on
uint16_t modelNumber;              //The Model Number of the Node
uint16_t modelOption;              //The Model Option of the Node
uint32_t serial;                   //The Serial Number of the Node
uint16_t firmwareVersion1;         //The Firmware Version of the Node (part 1)
uint16_t firmwareVersion2;         //The Firmware Version of the Node (part 2)
uint16_t defaultMode;              //The Default Mode of the Node
uint32_t bitResult;                //Built In Test result
int8_t reserved;                   //RESERVED
int8_t baseRssi;                   //Base Station RSSI
uint16_t checksum;                 //Checksum of [stopFlag - model]
```
**modelNumber** - The main model of the Node (ex. 6305 = G-Link).

**modelOption** - The specific option of the model. Combine this with the modelNumber to accurately identify the Node (ex. 6305-2000 = G-Link 2G, 6305-3000 = G-Link 10G).

**firmwareVersion** - The firmware version of the Node. Byte 1 is the Major part, while Bytes 2-4 (as a uint32_t) together represent the Minor part.


## Beacon Echo Packet
For BaseStation's with Firmware v3.32+, writing a `2` to EEPROM 40 will enable any beacon packets that are sent from the BaseStation to be echoed over the port.

```cpp
uint8_t startByte           = 0xAA;     //Start of Packet Byte
uint8_t stopFlag            = 0x07;     //Delivery Stop Flag
uint8_t appDataType         = 0x10;     //App Data Type
uint16_t address            = 0x0000;   //Address
uint8_t payloadLen          = 0x06;     //Payload Length
uint16_t cmd                = 0xBEAC;   //Command
uint32_t timestampSec;                  //Beacon's UTC Timestamp (seconds)
int8_t reserved;                        //RESERVED
int8_t reserved;                        //RESERVED
uint16_t checksum;                      //Checksum of [stopFlag - reserved]
```
**timestampSec** - The timestamp (seconds since Unix Epoch) of the beacon.

## RF Sweep Packet
Contains radio frequency information. This is sent when the BaseStation is in RF Sweep Mode.

```cpp
uint8_t startByte           = 0xAA;     //Start of Packet Byte
uint8_t stopFlag            = 0x07;     //Delivery Stop Flag
uint8_t appDataType         = 0x31;     //App Data Type
uint16_t address            = 0x1234;   //Address
uint8_t payloadLen;                     //Payload Length
uint8_t id                  = 0;        //ID, reserved for future use
uint32_t minFreq;                       //Minimum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t maxFreq;                       //Maximum Sweep Frequency in kHz (2400000 = 2.4GHz)
uint32_t interval;                      //The Sweep interval in kHz.
uint8_t data[];                         //The rssi data values for each frequency (in negative dBm)
int8_t reserved;                        //RESERVED
int8_t reserved;                        //RESERVED
uint16_t checksum;                      //Checksum of [stopFlag - data]
```
