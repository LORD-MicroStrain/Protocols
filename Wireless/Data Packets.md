# Wireless Data Packets

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
