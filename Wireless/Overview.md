# MicroStrain Wireless Protocol


## Overview

The MicroStrain Wireless Protocol describes how to communicate at a low level with devices that make up the MicroStrain Wireless product line.

This includes [BaseStations](http://www.microstrain.com/wireless/gateways) and [Wireless Nodes](http://www.microstrain.com/wireless/sensors).

Most users who want to write their own code to interact with MicroStrain devices should check out [MSCL (MicroStrain Communication Library)](http://lord-microstrain.github.io/MSCL/). MSCL abstracts all of the low-level logic and provides an easy to use, unit tested, high-level interface to communicate with our devices. It can be used in C++, C#, Python, and LabView.

For users who do not wish to use MSCL, this protocol should provide all the information you need to get up and running with writing your own software.

## Interface

### USB:
When communicating with a WSDA-Base Station via USB, a virtual serial port is created using the [Silicon Labs CP210x USB to UART Bridge VCP driver](https://www.silabs.com/products/mcu/Pages/USBtoUARTBridgeVCPDrivers.aspx).

The following settings should be used:
<br>**Baud Rate**: 921600
<br>**Parity**: None
<br>**Data Bits**: 8
<br>**Stop Bits**: 1

### RS-232:
When communicaing with a WSDA-Base Station and the host computer via RS-232, the physical layer provides the interface and there is no driver required by the Base Station.

The following settings should be used:
<br>**Baud Rate**: 115200 (default) or 921600 (device configurable)
<br>**Parity**: None
<br>**Data Bits**: 8
<br>**Stop Bits**: 1

## Endianness

All commands, responses, and data are in **Big Endian**.<br>
Therefore, when building a field that is more than 1 byte, the Most Significant Byte (MSB) is the first byte (smallest address), and the Least Significant Byte (LSB) is the last byte.

**2-byte value example (uint16):**

|            | Decimal   | Hex     | Binary |
| :----------:   | :-------: | :-----: | :-----------------: |
| 2-byte value   | 476       | 01 DC   | 00000001 1101100 |
| MSB            | 1         | 01      | 00000001 |
| LSB            | 220       | DC      | 1101100 |


```cpp
//Sample Code (C++) for 2-byte conversion

void ValueToMSBandLSB(uint16_t value, uint8_t& msb, uint8_t& lsb)
{
    msb = value >> 8;     //Shift 8 bits right, drop the lower byte.
    lsb = value & 0x00ff; //Mask out the upper byte.
}

uint16_t ValueFromMSBandLSB(uint8_t msb, uint8_t lsb)
{
    return (msb << 8) | lsb; //Shift msb 8 bits left, then OR the lsb in.
}
```

**4-byte value example (uint32):**

|            | Decimal       | Hex         | Binary 
|:----------:|:-------------:|:-----------:|:-----------------:
|2-byte value| 1,326,214,446 | 4F 0C 6D 2E | 01001111 00001100 01101101 00101110
|Byte 1 (MSB)| 79            | 4F          | 01001111
|Byte 2      | 12            | 0C          | 00001100
|Byte 3      | 109           | 6D          | 01101101
|Byte 4 (LSB)| 46            | 2E          | 00101110

```cpp
//Sample Code (C++) for 4-byte conversion

void ValueTo4Bytes(uint32_t value, uint8_t& b1, uint8_t& b2, uint8_t& b3, uint8_t& b4)
{
    b1 = value >> 24;          //Shift 24 bits right, drop lower bytes
    b2 = (value >> 16) & 0xff; //Shift 16 bits right, drop lower bytes, Mask out the upper bytes

    b3 = (value >> 8) & 0xff;  //Shift 8 bits right, drop lower byte, Mask out the upper bytes
    b4 = value & 0xff;         //Mask out the upper bytes
}

uint32_t ValueFrom4Bytes(uint8_t b1, uint8_t b2, uint8_t b3, uint8_t b4)
{
    uint16_t hiWord = (b1 << 8)| b2;    //Shift msb 8 bits left, then OR the lsb in.
    uint16_t loWord = (b3 << 8)| b4;    //Shift msb 8 bits left, then OR the lsb in.

    return (hiWord << 16) | loWord; //Shift hiWord 16 bits left, then OR the loWord in.
}
```
## RSSI

The Received Signal Strength Indicator (RSSI) is a measurement of the power present in a received radio signal.  Node commands such as Long Ping and Node Discovery return a true RSSI value, measured in dBm, in their response packet.  This signed 1-byte value can range from -95 dBm (worst) to +5 dBm (best). 

Some command responses return two RSSI values, **Node RSSI** and **Base Station RSSI**.<br>
The **Node RSSI** is the signal strength that the node received the command from the base station.<br>
The **Base Station RSSI** is the signal strength that the base station received the response back from the node.

## Checksums

Most commands and responses require or supply a checksum.  The checksum is used to ensure that the data was transmitted without error.  The documentation for each command or response that uses a checksum will detail how the checksum is calculated.  The checksum is calculated by summing all the bytes protected by the checksum and taking the modulo N of the sum, where N is 256 for a 1 byte checksum and 65536 for a 2 byte checksum.

```cpp
//Sample Code (C++) for calculating a checksum

uint8_t byte1 = 10;
uint8_t byte2 = 121;
uint8_t byte3 = 37;
uint8_t byte4 = 235;

//in C++, using the correct types (uint16_t) will automatically "wrap" for you,
//so just adding the bytes together will product the correct checksum.
uint16_t sum = byte1 + byte2 + byte3 + byte4;

//if you can't use the strict uint16_t type, you will have to perform the mod manually.
uint32_t sum2 = (byte1 + byte2 + byte3 + byte4) % 65535;
```
