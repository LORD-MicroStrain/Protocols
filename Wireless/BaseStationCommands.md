# Base Station Commands

**List of Commands:**

* [Ping Base Station](#ping-base-station)
* [Read EEPROM](#read-base-station-eeprom)
* [Write EEPROM](#write-base-station-eeprom)
* [Enable Beacon](#enable-beacon)
* [Disable Beacon](#disable-beacon)


## Ping Base Station

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
## Read Base Station EEPROM

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
## Write Base Station EEPROM

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
## Enable Beacon

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
## Disable Beacon

The Disable Beacon command is used to turn off the beacon on the Base Station. Sending the Stop Node command from the Base Station that is beaconing will automatically turn off the beacon as well.

##### Command:
```cpp
uint16_t commandId 				= 0xBEAC;		//Command ID
uint32_t disableBeaconValue 	= 0xFFFFFFFF;	//Value to disable the beacon
```

##### Success Response:
```cpp
uint16_t commandId 			    = 0xBEAC;		//Command ID Echo
```
##### Fail Response:
None.

##### Notes:
Notice that the **Disable Beacon** command packet is the same as the Enable Beacon command packet, but with 0xFFFFFFFF for its "Timestamp" bytes.
